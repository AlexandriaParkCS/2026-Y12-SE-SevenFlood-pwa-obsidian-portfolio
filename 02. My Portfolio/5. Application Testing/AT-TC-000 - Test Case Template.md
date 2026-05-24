# Test Cases

These test cases are based on the implemented Flask application in `2026-Y12-SE-SevenFlood-pwa-flask-application`.

## Test Case 001

**Test Case ID:** TC-001

**Description:** Verify that a new customer can create an account.

**Preconditions:**
- The Flask app is running.
- The Sign Up page is accessible at `/signup.html`.
- The username and email have not already been registered.

**Steps:**
1. Open `/signup.html`.
2. Enter a valid username, email and strong password.
3. Leave the account type as customer.
4. Submit the form.

**Test Data:**
- Username: `testcustomer`
- Email: `testcustomer@example.com`
- Password: `StrongPass1!`

**Expected Result:** The account is created, the password is stored as a hash, a session starts and the user is redirected to `/dashboard.html`.

## Test Case 002

**Test Case ID:** TC-002

**Description:** Verify that weak sign-up data is rejected.

**Preconditions:**
- The Sign Up page is accessible.

**Steps:**
1. Open `/signup.html`.
2. Enter a short username, invalid email or weak password.
3. Submit the form.

**Test Data:**
- Username: `ab`
- Email: `not-an-email`
- Password: `pass`

**Expected Result:** The account is not created and validation errors are shown.

## Test Case 003

**Test Case ID:** TC-003

**Description:** Verify that a customer can log in with valid credentials.

**Preconditions:**
- A customer account exists.
- The Login page is accessible at `/login.html`.

**Steps:**
1. Open `/login.html`.
2. Enter the registered username and password.
3. Submit the form.

**Test Data:**
- Username: `testcustomer`
- Password: `StrongPass1!`

**Expected Result:** The user is logged in and redirected to the dashboard.

## Test Case 004

**Test Case ID:** TC-004

**Description:** Verify that an incorrect password does not log the user in.

**Preconditions:**
- A customer account exists.

**Steps:**
1. Open `/login.html`.
2. Enter a valid username and incorrect password.
3. Submit the form.

**Test Data:**
- Username: `testcustomer`
- Password: `WrongPass1!`

**Expected Result:** The user stays on the login page and sees a generic error message.

## Test Case 005

**Test Case ID:** TC-005

**Description:** Verify that staff/admin can add points to a customer account.

**Preconditions:**
- A staff or admin account is logged in.
- A customer exists in the same cafe.

**Steps:**
1. Open `/admin.html`.
2. Search for the customer.
3. Select the action to add 10 points.
4. Open the customer's history.

**Test Data:**
- Points added: `10`

**Expected Result:** The customer's points increase by 10 and a `points_earned` transaction is recorded.

## Test Case 006

**Test Case ID:** TC-006

**Description:** Verify that a customer can redeem a reward when they have enough points.

**Preconditions:**
- A customer is logged in.
- The customer has at least 100 points.
- Active rewards exist in the database.

**Steps:**
1. Open `/redeem.html`.
2. Choose the Free coffee reward.
3. Submit the redeem form.
4. Open `/history.html`.

**Test Data:**
- Reward: `Free coffee`
- Cost: `100` points

**Expected Result:** The reward is redeemed, 100 points are removed and a `reward_redeemed` transaction appears in history.

## Test Case 007

**Test Case ID:** TC-007

**Description:** Verify that a customer cannot redeem a reward without enough points.

**Preconditions:**
- A customer is logged in.
- The customer has fewer points than the selected reward cost.

**Steps:**
1. Open `/redeem.html`.
2. Select a reward that costs more than the current points balance.
3. Submit the redeem form.

**Test Data:**
- Current points: `20`
- Reward cost: `100`

**Expected Result:** A warning message explains how many more points are needed and the user's balance does not change.

## Test Case 008

**Test Case ID:** TC-008

**Description:** Verify that a customer cannot access staff/admin pages.

**Preconditions:**
- A customer account is logged in.

**Steps:**
1. Open `/admin.html`.

**Test Data:**
- Role: `customer`

**Expected Result:** Access is blocked with forbidden access.

## Test Case 009

**Test Case ID:** TC-009

**Description:** Verify that PWA files load correctly.

**Preconditions:**
- The Flask app is running.

**Steps:**
1. Open the app in a browser.
2. Check that `/static/manifest.json` loads.
3. Check that `/service-worker.js` loads from the app root.
4. Simulate offline navigation after cached pages load.

**Test Data:**
- Browser: Chrome or Edge

**Expected Result:** The manifest loads, the service worker registers and cached pages or `/offline.html` appear when offline.
