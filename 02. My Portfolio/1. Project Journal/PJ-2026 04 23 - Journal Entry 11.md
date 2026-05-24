# Project Journal

**Date:** 23 Apr 2026  
**Project:** Loyal Cafe Rewards PWA  
**Module:** PWA features and offline support

## What I Did

- Added a web app manifest.
- Added app icons and screenshot assets.
- Added a service worker file.
- Added an offline page.
- Registered the service worker at the app root with `/service-worker.js`.

## Why I Did It

The project is a PWA, so it needs more than normal web pages. The app should feel installable and should handle offline or poor network situations better than a basic website.

## Challenges

The challenge was service worker scope. If the service worker is only registered under a static folder, it cannot control the full app properly.

## How I Solved Them

I added a Flask route for `/service-worker.js` and used the `Service-Worker-Allowed: /` header. This lets the service worker control the whole app scope.

## Next Steps

- Test the manifest and service worker in a browser.
- Check the app on mobile width.
- Add Lighthouse testing later for PWA evidence.

## Reflection

This stage helped the project meet the PWA requirement. I learned that PWA features need correct configuration, not just a manifest file.
