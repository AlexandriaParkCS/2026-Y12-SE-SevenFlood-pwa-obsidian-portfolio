# Code Repository

Application repository:

[2026-Y12-SE-SevenFlood-pwa-flask-application](https://github.com/SevenFlood/2026-Y12-SE-SevenFlood-pwa-flask-application)

Portfolio repository:

[2026-Y12-SE-SevenFlood-pwa-obsidian-portfolio](https://github.com/SevenFlood/2026-Y12-SE-SevenFlood-pwa-obsidian-portfolio)

## Current Application Commit Evidence

The Flask application repository currently shows these commits:

| Commit | Message | Evidence |
| --- | --- | --- |
| `dce96ce` | Initial commit | Started the Flask PWA application repository. |
| `557d36d` | login, signup html and update code for app and data | Added login/sign-up pages and updated application/database code. |
| `5c81402` | changes done ages ago | Added further application changes. The message could be improved because it does not clearly explain the work. |
| `9f5d4ed` | logining in to the dash broad | Added login flow into the dashboard. The message should be corrected in future commits for professionalism. |

## Code Progress Completed

The current Flask application includes:

- `src/app.py`: Flask routes for home, sign-up, login, logout, dashboard, admin, reward redemption, history, privacy, offline page and service worker.
- `src/data.py`: SQLite database access class with tables for cafes, users, rewards and transactions.
- `src/templates/`: HTML templates for the main user screens, admin screens, history and reward redemption.
- `src/static/manifest.json`: PWA install metadata, app icons, screenshots and shortcuts.
- `src/static/js/serviceWorker.js`: service worker caching and offline support.
- `src/static/js/app.js`: install prompt and reward reminder hooks.
- `src/static/css/style.css`: responsive cafe-themed styling.

## Security And Quality Progress

The implementation includes several important improvements:

- Passwords are stored with Werkzeug password hashing.
- Login, signup, logout, admin actions and reward redemption use CSRF protection.
- Flask sessions use safer cookie settings.
- A Content Security Policy is added to responses.
- SQL queries use parameter binding.
- Staff/admin routes check user roles before allowing access.
- Public signup prevents new staff/admin accounts after an admin exists.

## PWA Progress

The app includes PWA features:

- Web app manifest.
- App icons and screenshots.
- Root-scoped service worker route at `/service-worker.js`.
- Offline page at `/offline.html`.
- Cached app shell and static assets.
- Mobile-friendly layouts.

## Screenshots Evidence

The Flask application contains screenshot assets that can be used as portfolio evidence:

- `src/static/icons/desktop_screenshot.png`
- `src/static/icons/mobile_screenshot.png`

More screenshots should be added after final testing, especially the home page, sign-up page, dashboard, rewards page, history page and admin panel.

## Reflection

The application has progressed from a simple loyalty card idea into a working Flask and SQLite PWA. The biggest challenge was making it more secure and realistic, because a loyalty system needs login protection, hashed passwords, role checks, transaction history and reward validation. I solved this by adding CSRF protection, password hashing, staff/admin routes and a normalised database. Future commit messages should be clearer and more regular so the GitHub history proves the development process more strongly.
