# Project Journal

**Date:** 16 Apr 2026  
**Project:** Loyal Cafe Rewards PWA  
**Module:** Staff and admin tools

## What I Did

- Added staff/admin pages for managing customers.
- Allowed staff/admin users to search customer accounts.
- Added actions for adding 10 points and resetting customer points.
- Added customer history access for staff/admin users.

## Why I Did It

A real cafe loyalty system needs staff tools, not just customer pages. Staff need a way to add points after purchases and check a customer's account history.

## Challenges

The main challenge was preventing normal customers from accessing staff pages. If role checks are missing, customers could change points themselves.

## How I Solved Them

I added role checks for staff and admin routes. Customer accounts are blocked from admin pages, and staff can only manage customers they are allowed to manage.

## Next Steps

- Test staff/admin permissions.
- Check that point changes create transaction records.
- Improve the admin page layout and messages.

## Reflection

This stage made the project more realistic as a business application. It also made security more important because staff tools can change customer data.
