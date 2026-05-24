# Project Journal

**Date:** 3 Mar 2026  
**Project:** Loyal Cafe Rewards PWA  
**Module:** Database planning

## What I Did

- Planned the database for the loyalty application.
- Identified the main data needed: users, cafes, rewards and transactions.
- Changed the idea from only using a stamp card to using a points system.

## Why I Did It

The app needs a database so it can remember customer accounts, points balances, rewards and activity history. A points system also makes the app more flexible than a paper punch card.

## Challenges

The challenge was deciding whether to store only the current points balance or also store each action that changed the points.

## How I Solved Them

I decided to include a transactions table. This means the app can show a history of points earned, points reset and rewards redeemed, instead of only showing the current balance.

## Next Steps

- Build the SQLite database tables in the Flask app.
- Add functions for creating users and reading account data.
- Make sure passwords are not stored in plain text.

## Reflection

This stage improved the project because it made the app more realistic. A real business would need to see customer activity, not just the final points number.
