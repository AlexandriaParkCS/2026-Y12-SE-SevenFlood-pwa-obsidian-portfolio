Project Overview
Loyal Cafe is a web-based progressive web application (PWA) designed to replace paper-based coffee loyalty cards with a digital, multi-cafe loyalty points system. Customers earn 10 points per coffee purchase, track their balance across multiple participating cafes, and redeem points for rewards such as a free coffee (100 points) or a free muffin (60 points). The application is developed using Python and Flask with a SQLite database and is designed to be installable on mobile devices without requiring an app store.

Problem Statement
Small independent cafes typically rely on paper loyalty cards, which are easily lost, damaged, or duplicated. Customers cannot track their progress digitally, and staff have no visibility into loyalty activity across their customer base. Loyal Cafe solves these problems by providing a secure, lightweight digital loyalty platform that requires no native app development and can be self-hosted at minimal cost.

Objectives
•	Allow customers to create accounts and earn loyalty points at one or more participating cafes.
•	Provide staff and admin users with a management panel to search customers, add purchase points, and review account history.
•	Enable customers to redeem points for rewards directly from their phone via the PWA.
•	Implement security best practices including CSRF protection, bcrypt password hashing, parameterised SQL queries, and a Content Security Policy.
•	Support offline access via a service worker so the app is usable when the device is temporarily offline.
•	Keep infrastructure costs at or near zero using free open-source tools and free-tier hosting.
