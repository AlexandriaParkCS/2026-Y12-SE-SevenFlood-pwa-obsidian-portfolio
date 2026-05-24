# Test Report

**Test Date:** 20/05/2026

## Results

These results document the current Flask application evidence from `2026-Y12-SE-SevenFlood-pwa-flask-application`.

| Test Case | Outcome | Notes |
| --- | --- | --- |
| TC-001 Account creation | Pass | Valid sign-up creates a user, hashes the password and redirects to the dashboard. |
| TC-002 Signup validation | Pass | Invalid email, weak password and invalid usernames are rejected. |
| TC-003 Login | Pass | Valid username and password start a session and load the dashboard. |
| TC-004 Login security | Pass | Incorrect passwords show a generic error and do not start a session. |
| TC-005 Staff/admin add points | Pass | Staff/admin users can add 10 points and create a transaction record. |
| TC-006 Reward redemption | Pass | Customers with enough points can redeem a reward and points are deducted. |
| TC-007 Reward validation | Pass | Customers without enough points receive a warning and balance does not change. |
| TC-008 Admin protection | Pass | Customer accounts are blocked from staff/admin pages. |
| TC-009 PWA files | Pass | Manifest, service worker route, icons, screenshots and offline page are included. |

## Bugs Found And Fixed

| Bug or issue | How it was found | Fix made |
| --- | --- | --- |
| Transaction history query had ambiguous joined columns. | SQLite smoke testing while checking earned and redeemed points. | Qualified joined columns and ordered by transaction date. |
| Rewards were hard-coded instead of stored in the database. | Database design review. | Added a `rewards` table and linked reward redemptions to `reward_id`. |
| Service worker scope was too narrow. | PWA review. | Added `/service-worker.js` Flask route with root scope and `Service-Worker-Allowed: /`. |
| Logout used a GET link. | Security review. | Changed logout to a POST-only CSRF-protected form. |
| Public signup could expose privileged roles. | Security review. | Restricted staff/admin self-registration after an admin exists. |
| Mobile spacing on signup was inconsistent. | Visual review. | Improved form spacing with CSS. |

## Screenshot Evidence

The Flask application includes PWA screenshot assets:

- `src/static/icons/desktop_screenshot.png`
- `src/static/icons/mobile_screenshot.png`

Additional final portfolio screenshots should be added for the sign-up page, dashboard, rewards page, history page and admin page after the app is run in the browser.

## Reflection

Testing improved both functionality and security. The biggest challenge was not only checking that pages loaded, but checking that important actions updated the database correctly. I solved this by testing the full process: account creation, login, point changes, reward redemption and transaction history. Future testing should include Lighthouse scores, real phone testing and feedback from classmates or family members.

