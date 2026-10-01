FMS - FLEET FINANCIAL MANAGEMENT SYSTEM (multi-company)
Files: index.html, config.js, firebase-rules.json, manifest.webmanifest, sw.js, icon-192.png, icon-512.png

1. DEPLOY
   New GitHub repo (e.g. fms), upload all files, then Netlify > Import from GitHub (build settings empty).
   Out of the box it is in DEMO MODE: data stays in one browser and is NOT secure. Use it only to try the screens.

2. GO LIVE (secure, shared) - free Firebase account, easiest on a computer
   a. console.firebase.google.com > Add project.
   b. Build > Realtime Database > Create database (locked mode).
   c. Rules tab: paste the whole content of firebase-rules.json, then Publish.
   d. Build > Authentication > Get started > Email/Password > Enable.
   e. Authentication > Users > Add user: your ADMIN email + password. Copy that user's UID.
   f. Realtime Database > Data: add child  admins  with a child named by that UID and value  true
   g. Project settings (gear) > General: copy the Web API Key. Copy the database URL from the Data tab.
   h. Edit config.js, paste both values, commit. Netlify redeploys.

3. HOW IT WORKS
   Admin tab: approve, suspend, open or delete companies.
   Company: Register tab gives a Company ID (like C12345). Admin approves. Then sign in with Company ID + User ID + password.
   Workers: the Owner creates them in Staff, then taps Rights to choose per section: None / View only / View and edit.
   Starting levels: Owner, Manager, Accountant, Viewer, Driver.
   Tabs: Live map, Dashboard, Assets, Vehicle costs, Trips, Drivers (documents and reminders), Driver stats, My fleet, Ledger, Rates, Reports, Staff.
   Asset types: Truck, Bus, Rental car, InDrive car, Other.

4. LIMITS - PLEASE READ
   - Live map shows each asset's LAST RECORDED position from imported reports. Ignition and heading are worked out from trip data.
     True live tracking needs a GPS feed (for example the TrackGlo API) to be connected later.
   - Driver PDFs are limited to 600 KB each and are stored inside the database.
   - I could not test the rules or live login against a real Firebase project. Test with two practice companies first (Rules Playground).
   - Passwords cannot be reset from the app. Remove the worker and create a new login.
   - Download buttons are hidden without the Downloads right, but anyone with View rights can read that data.
   - Drivers cannot yet be limited to only their own vehicle.
