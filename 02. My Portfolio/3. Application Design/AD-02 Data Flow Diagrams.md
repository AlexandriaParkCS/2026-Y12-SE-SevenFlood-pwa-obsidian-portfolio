# Data Flow Diagrams

These diagrams are based on the current Flask application in `2026-Y12-SE-SevenFlood-pwa-flask-application`.

## Level 0 Context Diagram

```mermaid
flowchart LR
    Customer[Customer]
    Staff[Staff or Admin]
    System[Loyal Cafe Rewards PWA]
    Database[(SQLite Database)]

    Customer -->|Sign up, login, view dashboard, redeem rewards, view history| System
    System -->|Points balance, reward progress, history and messages| Customer
    Staff -->|Search customers, add points, reset points, view customer history| System
    System -->|Customer results and account updates| Staff
    System -->|Read and write cafes, users, rewards and transactions| Database
```

## Level 1 Data Flow Diagram

```mermaid
flowchart TD
    Customer[Customer]
    Staff[Staff or Admin]
    Users[(users)]
    Cafes[(cafes)]
    Rewards[(rewards)]
    Transactions[(transactions)]

    P1[1. Register or Login]
    P2[2. Show Dashboard]
    P3[3. Staff Manage Points]
    P4[4. Redeem Reward]
    P5[5. View History]
    P6[6. PWA Offline Support]

    Customer -->|username, email, password, selected cafe| P1
    P1 -->|hashed account details| Users
    P1 -->|new cafe for first admin| Cafes
    Users -->|verified session| P2
    P2 -->|points and reward progress| Customer

    Staff -->|search text and selected customer| P3
    P3 -->|customer lookup| Users
    P3 -->|points earned or reset| Users
    P3 -->|audit record| Transactions
    P3 -->|update result| Staff

    Customer -->|selected reward| P4
    P4 -->|reward cost and active status| Rewards
    P4 -->|deduct points if enough balance| Users
    P4 -->|reward redemption record| Transactions
    P4 -->|success or warning message| Customer

    Customer -->|history request| P5
    P5 -->|joined transaction and reward data| Transactions
    Rewards -->|reward names| P5
    P5 -->|ordered transaction history| Customer

    Customer -->|install or revisit app| P6
    P6 -->|cached shell and offline page| Customer
```

## Reflection

The original idea was a simple digital stamp card, but the Flask implementation became a points-based loyalty system. This made the design stronger because points, rewards and transactions can all be tracked in the database. The main challenge was keeping customer actions separate from staff/admin actions, so the data flow diagram now shows both user groups clearly.
