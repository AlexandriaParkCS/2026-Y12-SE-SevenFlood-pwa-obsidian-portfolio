# Project Journal

**Date:** 24 Mar 2026  
**Project:** Loyal Cafe Rewards PWA  
**Module:** Login and session management

## What I Did

- Built the login page and login route.
- Checked the user's password against the stored password hash.
- Created a Flask session after successful login.
- Added logout as a POST form instead of a simple link.

## Why I Did It

The app needs login so customers can securely access their own dashboard and points. Logout is also important so users can leave their account safely.

## Challenges

The challenge was making login secure without giving too much information to attackers. For example, the app should not tell someone whether the username or password was the wrong part.

## How I Solved Them

I used a generic error message for failed login attempts. I also used safer session settings and changed logout to a POST action protected by CSRF.

## Next Steps

- Build the dashboard.
- Show the user's current points.
- Add reward progress so the user can see how close they are to a reward.

## Reflection

This stage showed me that account systems need careful handling. Login is not just about checking a password; it also needs sessions, redirects, logout and clear error handling.
