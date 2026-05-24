AD-03 Structure Chart

Login Process
The Login process is responsible for authenticating existing users and establishing a secure browser session. It is triggered when a registered user submits the login form at /login.html. The process validates the submitted credentials, queries the database, and either creates a session and redirects to the dashboard or returns an error to the user.

Structure Chart – Login

[Login]
  ├── [Validate Input]
  │     ├── Normalise username (strip, truncate to 30 chars)
  │     └── Check username matches USERNAME_PATTERN ([A-Za-z0-9_]+)
  ├── [Verify Credentials]
  │     ├── get_user_by_username(username)  →  User record or None
  │     └── check_password_hash(stored_hash, submitted_password)
  ├── [Create Session]
  │     ├── session.clear()
  │     ├── Store user_id, username, role, cafe_id, active_cafe_id
  │     └── session.permanent = True  (2-hour lifetime)
  └── [Respond]
        ├── Success → redirect to /dashboard.html
        └── Failure → render login.html with error message

The top-level Login module coordinates three sub-modules. Validate Input sanitises and pattern-checks the submitted username before any database call is made, preventing malformed data from reaching the query layer. Verify Credentials queries the users table by username and uses Werkzeug's check_password_hash to compare the submitted password against the stored bcrypt hash without ever exposing the raw hash. Create Session writes the authenticated user's details into a server-side Flask session with a two-hour lifetime, setting the HttpOnly and SameSite=Lax cookie flags. Finally, Respond either redirects the user to their dashboard or re-renders the login page with a generic error.

Algorithms

BEGIN Login
  username = NormaliseText(form.username, maxLength=30)
  IF NOT MatchesPattern(username, '[A-Za-z0-9_]+')
    DISPLAY 'Incorrect username or password'
    END
  ENDIF
  user = GetUserByUsername(username)
  IF user IS NULL
    DISPLAY 'Incorrect username or password'
    END
  ENDIF
  passwordMatches = CheckPasswordHash(user.password, form.password)
  IF NOT passwordMatches
    DISPLAY 'Incorrect username or password'
    END
  ENDIF
  CreateLoginSession(user)
  REDIRECT to Dashboard
END

BEGIN GetUserByUsername(username)
  query = SELECT users.*, cafes.name AS cafe_name
          FROM users LEFT JOIN cafes ON users.cafe_id = cafes.id
          WHERE users.username = username
  row = ExecuteQuery(query)
  IF row IS NULL
    RETURN NULL
  ENDIF
  RETURN UserFromRow(row)
END

BEGIN CreateLoginSession(user)
  session.clear()
  session.permanent = TRUE
  session['user_id']       = user.id
  session['username']      = user.username
  session['role']          = user.role
  session['cafe_id']       = user.cafe_id
  session['active_cafe_id'] = user.cafe_id
END

Add Points Process
The Add Points process allows staff or admin users to record a coffee purchase against a customer's loyalty account at their cafe. It is triggered when an authorised staff member submits the +10 points form in the admin panel.

Structure Chart – Add Points (Staff)

[AddPoints]
  ├── [Authorise Staff]
  │     └── staff_required_user()  →  user or redirect
  ├── [Validate Request]
  │     ├── points_to_add must equal 10
  │     ├── staff must have a cafe_id
  │     └── customer_id must not equal staff user_id
  ├── [Verify Customer]
  │     ├── get_user_by_id(customer_id)
  │     └── can_manage_customer(staff, customer)
  ├── [Update Points]
  │     ├── INSERT OR IGNORE into customer_cafes
  │     ├── UPDATE customer_cafes SET points = points + 10
  │     └── INSERT transaction record
  └── [Respond]
        └── Redirect to admin panel with success message

BEGIN AddPoints
  user = StaffRequiredUser()
  pointsToAdd = form.points  (must equal 10)
  IF pointsToAdd != 10 OR user.cafe_id IS NULL
    REDIRECT to Dashboard
    END
  ENDIF
  customerID = form.user_id
  IF customerID == user.id
    REDIRECT to Dashboard  // Prevent self-award
    END
  ENDIF
  customer = GetUserByID(customerID)
  IF NOT CanManageCustomer(user, customer)
    REDIRECT to Admin with message='not-found'
    END
  ENDIF
  updatedUser = AddPoints(customerID, 10, 'Staff added points', user.id, user.cafe_id)
  REDIRECT to Admin with message='points-added'
END
