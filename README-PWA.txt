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
4. Your existing dashboard buttons continue to open the Google Apps Script URLs already present in the code.

OFFLINE BEHAVIOR:
The dashboard shell can open offline after the first successful visit. External Google Apps Script modules, Open-Meteo weather, and other external services still require internet access.

If you want the PWA URL to be your main production URL, replace your current bookmark/QR code with the hosted PWA URL.
