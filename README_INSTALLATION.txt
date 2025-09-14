Dante Snapshot Viewer — iPhone PWA Starter
=========================================

What this is
-------------
A production-ready scaffold to turn your existing Dante Snapshot Viewer HTML/JS into an iPhone installable web app (PWA).

Files
-----
- index.html                → Add your existing UI where marked (TODO block)
- manifest.webmanifest      → App metadata (name, icons, theme)
- service-worker.js         → Offline cache for the app shell
- offline.html              → Fallback page when offline
- assets/icon-192.png
  assets/icon-512.png
  assets/apple-touch-icon-180.png

How to integrate your viewer
----------------------------
1) Open index.html and find the block marked:
     <!-- TODO: Replace this entire block with your existing Dante viewer UI -->
   Replace that block with the HTML of your current viewer. Keep the <header> if you like its style.
2) Make sure any JS/CSS your viewer needs is referenced with relative paths (./assets/... or ./scripts/...).
3) If your viewer reads local Dante exports via the file picker, you're good. Service workers don't cache local files (privacy rules).

Serve over HTTPS
----------------
Service workers require HTTPS or localhost. Easiest options:
  - GitHub Pages (free, HTTPS by default)
  - Netlify / Vercel (free tiers)
  - Local: `python3 -m http.server 8080` then visit http://localhost:8080 (works on Mac/PC).

Install on iPhone (iOS 16.4+)
-----------------------------
  1) Open your app URL in Safari.
  2) Tap the Share button → "Add to Home Screen".
  3) Launch from the icon; it will run full screen. The app shell is cached for offline use.

Notes for iOS
-------------
  - iOS prefers the <link rel="apple-touch-icon"> even if icons exist in the manifest; we've included both.
  - Push notifications are optional and not set up here.
  - File inputs (via the Files app) work in PWAs; local files are never cached by SWs.

Versioning the cache
--------------------
  - Update CACHE_NAME in service-worker.js when you ship changes, or implement a build step that appends a hash to the cache name.

Troubleshooting
---------------
  - "Add to Home Screen" doesn’t appear: ensure Safari, not Chrome; ensure served over HTTPS; load the page once, then open Share.
  - SW doesn't register: check the URL is HTTPS or localhost; check console for errors.
  - App updates not showing: fully quit the PWA, reopen, or in Safari → Website Data → remove site data; bump CACHE_NAME.


Mobile UX enhancements included
-------------------------------
- Density toggle (Compact/Comfy) wired to <html> class.
- Sticky toolbar with large, thumb-friendly controls.
- Section expand/collapse with large hit targets + swipe gestures (left to collapse, right to expand).
- Responsive table scaffolding with sticky first column on wide screens.
- Horizontal scroll shadows for wide grids.
