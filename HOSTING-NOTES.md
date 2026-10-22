# Spec Sheet Builder: hosted version notes

Made October 21, 2026, from builder v13, to test hosting on Azure Static Web Apps.

## What changed from the Claude version
- **Starting data built in.** The brand list and logos, area and task library, Spanish translations, the four example specs, visuals and the floor plan images were copied into the file. On a browser's first visit they load automatically.
- **Saving goes to the browser.** Everything saves to that browser's own storage (IndexedDB). It stays on that one computer and browser. It is not shared between people, and clearing browser data erases it.
- **Downloads** (packets, PDFs, setup export) use a normal browser download.
- **The same file still works inside Claude.** If Claude's runtime is present, it uses Claude's storage as before.

## Not working in the hosted version yet
- Claude features: Import a spec, Ask Claude, Spanish translation, writing route card instructions. These need a server function that holds an Anthropic API key.
- Save to SharePoint, which went through Claude's Microsoft 365 connection.

## Moving to Airtable or Microsoft Lists later
All saving goes through one block of code marked **HOSTED-VERSION STORAGE LAYER** near the top of the main script. To switch, replace that block's database and image functions with calls to Airtable or Lists, through a small server function that keeps the access token secret. The rest of the app doesn't change.

Data the database needs to hold:
- `specs` — one record per spec
- `visuals` and `visualPhotos` — visual cards and their photos
- `config/library`, `config/brands`, `config/translations` — one record each
- Floor plan images (maps) — as attachments or files
