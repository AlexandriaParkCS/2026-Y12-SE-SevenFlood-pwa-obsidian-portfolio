# Data Dictionary

This data dictionary describes the implemented SQLite tables in the Flask application.

## cafes

| Attribute | Data Type | Bytes | Description | Example |
| --- | --- | --- | --- | --- |
| name | Text | Variable | Cafe name used to group staff and customers. | Loyal Cafe |
| created_by | Integer | 4 | User ID of the admin who created the cafe. | 1 |
| created_at | Text | Variable | Date and time the cafe was created. | 2026-05-20 10:30:00 |

## users

| Attribute | Data Type | Bytes | Description | Example |
| --- | --- | --- | --- | --- |
| username | Text | Variable | Unique account username. | testcustomer |
| email | Text | Variable | Unique email address for the account. | customer@example.com |
| password | Text | Variable | Werkzeug password hash, not a plain text password. | scrypt:32768... |
| points | Integer | 4 | Current loyalty point balance. | 80 |
| role | Text | Variable | User permission level. | customer |
| cafe_id | Integer | 4 | Cafe linked to the user account. | 1 |

## rewards

| Attribute | Data Type | Bytes | Description | Example |
| --- | --- | --- | --- | --- |
| code | Text | Variable | Unique reward code used by the app. | free-coffee |
| name | Text | Variable | Reward display name. | Free coffee |
| description | Text | Variable | Description shown on the rewards page. | Redeem a regular coffee made fresh at the counter. |
| points_cost | Integer | 4 | Points required to redeem the reward. | 100 |
| active | Integer | 1 | Whether the reward is currently available. | 1 |
| created_at | Text | Variable | Date and time the reward was created or seeded. | 2026-05-20 10:30:00 |

## transactions

| Attribute | Data Type | Bytes | Description | Example |
| --- | --- | --- | --- | --- |
| user_id | Integer | 4 | Customer account affected by the transaction. | 2 |
| reward_id | Integer | 4 | Reward linked to a redemption transaction. | 1 |
| performed_by_user_id | Integer | 4 | Staff/admin account that performed the action. | 1 |
| transaction_type | Text | Variable | Type of transaction recorded. | reward_redeemed |
| action | Text | Variable | Human-readable action shown in history. | Redeemed Free coffee |
| points_change | Integer | 4 | Positive or negative change to the user's points. | -100 |
| date | Text | Variable | Date and time the transaction occurred. | 2026-05-20 11:15:00 |

## Reflection

The data dictionary became more accurate after checking the actual Flask code. One design challenge was that the app tracks points directly on the user rather than using a separate loyalty card table. This is simpler for the current app, while the transactions table still keeps an evidence trail for points earned, points reset and rewards redeemed.
