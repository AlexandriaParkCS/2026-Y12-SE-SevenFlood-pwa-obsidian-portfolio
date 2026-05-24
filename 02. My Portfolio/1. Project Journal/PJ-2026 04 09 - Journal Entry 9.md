# Project Journal

**Date:** 9 Apr 2026  
**Project:** Loyal Cafe Rewards PWA  
**Module:** Rewards and redemption

## What I Did

- Added a rewards page that lists active rewards from the database.
- Added default rewards such as Free coffee and Free muffin.
- Built the reward redemption route.
- Recorded reward redemptions as transactions.

## Why I Did It

The reward system is the main purpose of the loyalty app. Customers need to exchange points for rewards, and the business needs a record of when this happens.

## Challenges

The challenge was preventing users from redeeming rewards without enough points. The app also needed to avoid hard-coding rewards only in Python.

## How I Solved Them

I added a rewards table and checked the user's points before redeeming. If the user has enough points, the app deducts the reward cost and records the redemption. If not, it shows a warning message.

## Next Steps

- Add transaction history so customers can see rewards and point changes.
- Test reward redemption with enough and not enough points.
- Improve messages shown after redeeming.

## Reflection

This stage made the app feel more complete because users can now do the main loyalty action. It also showed why database checks are important before changing a user's points.
