# Class Diagram

The current Flask app mainly uses route functions in `src/app.py` and a database access class in `src/data.py`. This diagram shows the implemented structure.

```mermaid
classDiagram
    class FlaskApp {
        +index()
        +signup()
        +login()
        +dashboard()
        +redeem()
        +redeem_reward()
        +history()
        +admin()
        +admin_add_points()
        +admin_reset_account()
        +service_worker()
    }

    class dataDb {
        +create_user()
        +verify_user()
        +get_user_by_id()
        +create_cafe()
        +get_all_cafes()
        +get_active_rewards()
        +add_points()
        +redeem_points()
        +reset_user_points()
        +get_transactions_by_user_id()
    }

    class UserRecord {
        +id
        +username
        +email
        +password
        +points
        +role
        +cafe_id
    }

    class RewardRecord {
        +id
        +code
        +name
        +description
        +points_cost
        +active
    }

    class TransactionRecord {
        +id
        +user_id
        +reward_id
        +performed_by_user_id
        +transaction_type
        +action
        +points_change
        +date
    }

    FlaskApp --> dataDb
    dataDb --> UserRecord
    dataDb --> RewardRecord
    dataDb --> TransactionRecord
```

## Design Notes

The `dataDb` class is responsible for SQLite database operations. The Flask route functions handle user actions such as signing up, logging in, viewing the dashboard, redeeming rewards and staff/admin management.

## Reflection

The implementation uses a simple Flask structure instead of many separate model classes. This kept the project easier to understand for a school PWA, but a future improvement would be to split the routes into blueprints and move validation into smaller helper modules.
