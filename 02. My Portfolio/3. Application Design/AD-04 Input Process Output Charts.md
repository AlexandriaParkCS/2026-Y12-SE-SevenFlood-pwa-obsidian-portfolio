# AD-04 Input Process Output Charts

## Sign Up

The Sign Up process enables new users to create a loyalty account and optionally join or create a cafe at the point of registration. It handles three account types: customer, staff, and admin, each with different validation requirements.

|   |   |   |
|---|---|---|
|**Input**|**Process**|**Output**|
|Username (text, 3–30 chars)|Normalise: strip whitespace, truncate to 30|New user record in users table|
|Email address (text)|Validate against EMAIL_PATTERN regex|New customer_cafes record (if cafe selected)|
|Password (text, min 8 chars)|Validate: uppercase, lowercase, digit, symbol|New cafe record (admin accounts only)|
|Role (customer/staff/admin)|Check role is in VALID_ROLES; block staff/admin if admin already exists|Default rewards seeded for new cafe|
|Cafe ID (optional integer)|Verify cafe exists in cafes table|Authenticated session created|
|Cafe name (admin only)|Validate against CAFE_NAME_PATTERN; check uniqueness|Redirect to /dashboard.html|
|Cafe location (admin only)|Validate against LOCATION_PATTERN|Error messages returned on failure|
|Cafe logo path (admin only)|Validate starts with /static/; default to /static/images/logo.png||
|CSRF token (hidden field)|Verified by Flask-WTF before processing||

## Redeem Reward

The Redeem Reward process allows an authenticated customer to exchange accumulated loyalty points for a reward at their active cafe. Points are deducted atomically and a transaction record is created to maintain a complete audit trail.

|   |   |   |
|---|---|---|
|**Input**|**Process**|**Output**|
|reward_id (hidden form field)|Validate reward_id is a positive integer|Points deducted from customer_cafes.points|
|User session (user_id, active_cafe_id)|Retrieve active cafe from session|Transaction record inserted (type: reward_redeemed)|
|CSRF token (hidden field)|Verify CSRF token via Flask-WTF|Redirect to /redeem.html?status=success|
||Retrieve reward from rewards table, filtered by cafe_id|Error redirect if insufficient points|
||Check user.points >= reward.cost|Error redirect if reward not found|
||Atomically UPDATE customer_cafes SET points = points - cost WHERE points >= cost||
||INSERT transaction (points_change = -cost, type = reward_redeemed)||

## Transaction History

The Transaction History process retrieves and displays a chronological record of all points earned and rewards redeemed by the current user at their active cafe.

|   |   |   |
|---|---|---|
|**Input**|**Process**|**Output**|
|User session (user_id)|Verify user is logged in via login_required_user()|Rendered history.html template|
|active_cafe_id (session)|Retrieve active cafe from session or first joined cafe|Table of transactions (date, cafe, action, points change)|
||Query transactions WHERE user_id = ? AND cafe_id = ?|Positive changes shown in green, negative in red|
||JOIN cafes, rewards, users (staff) tables for display names|Current points balance shown in header tile|
||ORDER BY date DESC, id DESC|Empty state message if no transactions exist|...