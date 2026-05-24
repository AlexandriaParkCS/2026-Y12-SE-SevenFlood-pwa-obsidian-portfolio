# Project Journal

**Date:** 7 May 2026  
**Project:** Loyal Cafe Rewards PWA  
**Module:** Testing and bug fixing

## What I Did

- Tested sign-up, login, logout, dashboard, reward redemption and history.
- Checked staff/admin point changes.
- Reviewed security issues such as CSRF, role protection and password storage.
- Fixed issues found during testing.

## Why I Did It

Testing proves that the app works as a full system. It also helps find problems that are not obvious when only looking at one page at a time.

## Challenges

One challenge was an ambiguous column problem in the transaction history query after joining tables. Another issue was making sure rewards were stored properly in the database instead of only being hard-coded.

## How I Solved Them

I qualified the transaction columns in the SQL query and linked reward redemptions to reward records. I also checked that point changes create transaction history, so the app has better evidence of user activity.

## Next Steps

- Add final screenshots to the portfolio.
- Run Lighthouse testing.
- Ask other people to test the app and record feedback.

## Reflection

Testing helped improve the quality of the project. It showed that small database or security problems can affect the whole user experience, so testing needs to happen throughout development.
