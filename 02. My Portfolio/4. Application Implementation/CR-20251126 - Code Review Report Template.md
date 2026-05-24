# Code Review Report

|   |   |
|---|---|
|**Field**|**Details**|
|Reviewer Name|Student Developer|
|Date|26 Nov 2025|
|Module / Feature|Loyal Cafe – Full Application (app.py, data.py, sqldb.py, HTML templates)|

## Code Summary

Loyal Cafe is a Flask-based progressive web application (PWA) that provides a multi-cafe loyalty points system. Customers earn points per coffee purchase, track their balance per cafe, and redeem rewards. Staff and admin users manage customers via a separate admin panel. The application uses a SQLite database (data.py), Jinja2 templates for HTML rendering, Flask-WTF for CSRF protection, and a Content Security Policy enforced via HTTP response headers.

## Strengths

•        CSRF protection is applied consistently across all POST forms using Flask-WTF, preventing cross-site request forgery attacks.

•        All database queries use parameterised statements (cursor.execute with ? placeholders), eliminating SQL injection vulnerabilities.

•        Passwords are stored as Werkzeug bcrypt hashes; plain-text passwords are never persisted.

•        Role-based access control (customer, staff, admin) is enforced at the route level using login_required_user(), staff_required_user(), and admin_required_user() helper functions.

•        A strict Content Security Policy is set via HTTP response headers in after_request, covering default-src, script-src, img-src, frame-src and form-action directives.

•        Input normalisation (normalise_text) and pattern validation (EMAIL_PATTERN, USERNAME_PATTERN, CAFE_NAME_PATTERN) are applied before any data reaches the database.

•        The PWA service worker, manifest, and offline fallback page are properly implemented, allowing the app to be installed on mobile devices.

•        Session cookies are configured with HttpOnly, SameSite=Lax, and an optional Secure flag controlled by an environment variable.

•        The data layer (data.py) uses a consistent _user_from_row, _cafe_from_row, and _transaction_from_row pattern, avoiding direct row access in business logic.

•        Database schema migrations are handled gracefully via _add_column_if_missing, avoiding breaking changes on existing databases.

## Issues Found

•        HIGH – Hardcoded secret key: app.secret_key = b'G6z115u8WnfQ0UIJ' is committed to source. If the repository is accessed by an unauthorised party, session cookies can be forged. Tracked as GitHub Issue #1.

•        MEDIUM – Plain-text password fallback in verify_user(): if bcrypt verification fails, the code compares the stored value directly against the submitted password, silently upgrading it. This creates a timing side-channel and accepts unhashed passwords from legacy data. Tracked as GitHub Issue #2.

•        MEDIUM – Staff self-award: the /add-points.html route does not check whether the target user_id matches the logged-in staff member's own ID, allowing staff to award points to themselves. Tracked as GitHub Issue #3.

•        MEDIUM – Duplicate logging configuration: data.py calls logging.basicConfig(stream=sys.stdout) and app.py calls logging.basicConfig(filename=...). The first call wins, so file-based logging in app.py silently fails. Tracked as GitHub Issue #4.

•        LOW – Logo URL not path-restricted: the cafe_logo field accepts any string up to 180 characters, including external URLs. While the CSP blocks external images in the browser, the value is stored and rendered without restriction. Tracked as GitHub Issue #5.

•        LOW – cursor not initialised before try in sqldb._create_tables: if the _connect() call raises an exception, the finally block references cursor before assignment, raising a NameError. Tracked as GitHub Issue #6.

•        LOW – Broken HTML pattern attribute in form.html: pattern='[a-z]{2, 4}$' contains a space inside the quantifier, making it an invalid regex. Browsers silently ignore invalid pattern attributes, disabling client-side email validation. Tracked as GitHub Issue #7.

•        LOW – CSP defined in both meta tag (layout.html) and HTTP response header (after_request). The HTTP header takes precedence, but the meta tag causes confusion and cannot support report-uri. Tracked as GitHub Issue #8.

•        INFO – privacy.html contained no content, presenting a compliance risk under the Australian Privacy Act 1988. Tracked as GitHub Issue #9.

•        INFO – loyalty.html template exists but is never rendered; the route only redirects to dashboard. Tracked as GitHub Issue #10.

## Recommendations

•        Load the Flask secret key from an environment variable using os.environ.get('SECRET_KEY') and raise a RuntimeError at startup if it is not set, preventing the application from running insecurely.

•        Remove the plain-text password fallback from verify_user() entirely. Any legacy plain-text passwords should be migrated via a one-off script run by an administrator.

•        Add a check in /add-points.html that rejects the request when the submitted user_id matches the session user's own ID.

•        Remove the basicConfig call from data.py and configure logging solely in app.py so file-based log output functions as intended.

•        Validate cafe_logo against a /static/ prefix allowlist before storing the value.

•        Initialise cursor = None before the try block in sqldb._create_tables to prevent a potential NameError in the finally clause.

•        Fix the pattern attribute in form.html: change {2, 4} to {2,4} to produce a valid HTML5 pattern regex.

•        Remove the <meta http-equiv='Content-Security-Policy'> tag from layout.html; rely solely on the HTTP header set by after_request.

•        Populate privacy.html with a complete privacy policy covering data collected, purpose, retention, security measures, and user rights.

•        Delete the unused loyalty.html template to reduce dead code in the repository.

## Overall Rating

Good – The application demonstrates strong security fundamentals with parameterised queries, CSRF protection, hashed passwords, and role-based access control throughout. The issues identified are mostly low-to-medium severity and correctable with targeted changes. Once the hardcoded secret key and password fallback are resolved, the application will be suitable for a controlled production deployment.