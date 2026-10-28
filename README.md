# School Gate Entry (static app, no Apps Script)

One file (`index.html`). Runs fully in the browser. Student data and entry records stay **on the gate device**.

## Host on GitHub Pages
1. Create a GitHub repository (name e.g. `gate-entry`) and upload `index.html` (and this README if you like).
2. **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `(root)` → Save.**
3. After a minute your app is live at `https://YOUR-USERNAME.github.io/gate-entry/` (HTTPS, so the camera prompt works).

**Do NOT upload your real student Excel file to the repo** — a public repo exposes it. Keep it on your computer/phone and load it in the app.

## Use at the gate
1. Open the URL on the gate phone/tablet → **⚙ Setup** → upload your Excel/CSV (`GR_No, Student_Name, Class, Section, Status`; first sheet, header in row 1). Status other than `Active` = rejected as inactive. Format the GR column as **Text** in Excel so leading zeros stay.
2. Fill in school, event, gate name, your name → **Save settings**.
3. **Start Camera** → Allow. Scan. Green = approved, red = rejected.
4. End of event: **Export entry log (Excel)**. For a new event: **Erase entry log**.

Test with `students_sample.csv`: GR1001 (approve, then duplicate), GR1003 (inactive), GR9999 (not found).

## QR codes
Each QR must contain only the GR number. In Excel/Sheets: `=IMAGE("https://api.qrserver.com/v1/create-qr-code/?size=300x300&data="&ENCODEURL(A2))`.

## Important limits (read this)
- **One gate device = one source of truth.** Entries are saved in that browser's storage. Two phones each have their own record, so the **same student could be approved once on each phone**. Duplicate prevention is guaranteed only per device (including multiple tabs on it, via a Web Lock). Use one gate device for entry, or give each gate a separate group of students.
- Clearing browser data, using private/incognito mode, or switching browsers loses the entries. Export the log regularly.
- Anyone using the device can open Setup and erase the log. Keep the device with staff.
- The page loads the QR and Excel libraries from jsDelivr, so the first load needs internet.
- Camera permission: allowed only on HTTPS (GitHub Pages) or `localhost`. If denied, tap the 🔒 icon → Camera → Allow → reload. "Scan from a photo" and manual entry work as backups.

## Need several gates at once?
That requires a shared online database (e.g. Firebase Firestore, free tier) with a transaction so only one device can create each GR's approval. The page can be extended to do this while staying on GitHub Pages.
