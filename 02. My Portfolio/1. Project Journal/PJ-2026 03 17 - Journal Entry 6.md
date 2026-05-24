# Project Journal

**Date:** 17 Mar 2026  
**Project:** Loyal Cafe Rewards PWA  
**Module:** Sign-up feature

## What I Did

- Built the sign-up page and route.
- Added username, email and password input fields.
- Added validation for usernames, emails and strong passwords.
- Connected new accounts to the SQLite database.

## Why I Did It

Customers need to create accounts so their points and rewards can be saved. Without sign-up, the loyalty card would not be personal to each user.

## Challenges

The biggest challenge was making the sign-up form secure enough. A simple form is easy to build, but it also needs to reject weak passwords and invalid data.

## How I Solved Them

I added validation rules and used Werkzeug password hashing. This means the database stores a password hash instead of the user's real password.

## Next Steps

- Build the login feature.
- Start a session after successful login.
- Redirect logged-in users to the dashboard.

## Reflection

This stage made the app feel more real because users could create an account. I also learned that security needs to be included early, not added only at the end.
