# Project Journal

**Date:** 20 May 2026  
**Project:** Loyal Cafe Rewards PWA  
**Module:** Portfolio evidence based on Flask application progress

## What I Did

- Updated the portfolio so it matches the actual work completed in `2026-Y12-SE-SevenFlood-pwa-flask-application`.
- Documented the implemented Flask routes for sign-up, login, dashboard, admin, rewards, history, offline page and service worker.
- Updated the database planning to match the real SQLite tables: cafes, users, rewards and transactions.
- Added testing evidence for account creation, validation, login, staff/admin point management, reward redemption, role protection and PWA files.
- Recorded the application Git commit history and reflected on how commit messages could be improved.

## Why I Did It

The portfolio needs to prove the real development process, not just describe what was planned. By connecting the portfolio to the Flask application repository, the evidence becomes more accurate and shows the actual progress made in code.

## Challenges

The main challenge was that some of the early portfolio wording described a simple stamp-card design, while the Flask app has developed into a points-based reward system with admin tools, security features and PWA support. The documentation needed to be updated so the design, database and testing sections all matched the real app.

## How I Solved Them

I checked the Flask app files, especially `src/app.py`, `src/data.py`, the templates, manifest and service worker. Then I rewrote the portfolio evidence so it explains the implemented features: hashed passwords, CSRF protection, role checks, reward redemption, transaction history, offline support and mobile screenshots.

## Future Improvements

- Add browser screenshots of each final page into the portfolio.
- Record Lighthouse results for PWA, accessibility, best practices and performance.
- Test on real iPhone and Android devices.
- Use clearer Git commit messages in future, such as `Add reward redemption history` instead of vague messages.
- Split the Flask app into smaller route or blueprint files if the code grows larger.

## Reflection

This stage improved the portfolio because it now reflects the actual Flask application instead of only the original plan. I learned that documentation must be updated when the design changes during development. The project is stronger because it now includes a working database, secure login, role-based staff features, PWA support and recorded testing evidence.
