SUPERVISOR DASHBOARD — PWA PACKAGE

This package keeps your existing dashboard UI and adds PWA support.

IMPORTANT — Google Apps Script:
Your current dashboard is served by Apps Script HtmlService. Google documents that HtmlService apps run in an IFRAME sandbox. Because a service worker must be registered from a normal secure web origin and the Apps Script page is sandboxed, the reliable setup is to host this PWA shell on a static HTTPS host (GitHub Pages, Cloudflare Pages, Firebase Hosting, etc.) and keep your existing Apps Script modules as the backend/apps.

Files:
- index.html — your original dashboard with PWA meta tags and service-worker registration added.
- manifest.json — install metadata.
- sw.js — app-shell cache and offline fallback.
- icons/ — 192px and 512px install icons.

DEPLOYMENT:
1. Upload the contents of this folder to an HTTPS static host.
2. Open the hosted index.html URL in Chrome/Edge.
3. Choose Install app / Add to Home Screen.
4. Your existing dashboard buttons now open the 7 Google Apps Script URLs INSIDE this PWA's window (an iframe with a "Home" bar), instead of handing off to a new browser tab. This keeps everything as one app/ecosystem when installed.

REQUIRED — ALLOW EMBEDDING IN EACH OF THE 7 APPS SCRIPT PROJECTS:
By default Google blocks Apps Script web apps from being loaded inside an iframe on another site (X-Frame-Options). To let the dashboard embed them, open each of the 7 Apps Script projects, find the function that returns the page (usually `doGet(e)`), and add `.setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)` to the returned HtmlOutput, e.g.:

  function doGet(e) {
    return HtmlService.createHtmlOutputFromFile('Index')
      .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL);
      // ...your existing .setTitle(), .addMetaTag(), etc. stay as-is
  }

Then redeploy each project (Deploy > Manage deployments > Edit > New version) so the change takes effect on the existing /exec URL — you do NOT need a new URL.

If a given app still won't load inside the frame after redeploying (e.g. it renders a Google login screen, which Google refuses to frame), the dashboard shows a "This app didn't load inside the dashboard — Open in browser instead" fallback link after ~9 seconds, so nothing is ever a dead end.

OFFLINE BEHAVIOR:
The dashboard shell can open offline after the first successful visit. External Google Apps Script modules, Open-Meteo weather, and other external services still require internet access.

If you want the PWA URL to be your main production URL, replace your current bookmark/QR code with the hosted PWA URL.
