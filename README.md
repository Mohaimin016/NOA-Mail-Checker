# AWB Mail Checker

Checks which **"Shipment Arrival Notification of &lt;AWB&gt;"** mails reached the group mailbox and which AWBs are **missing**.
It runs entirely in the browser: files you load are never uploaded anywhere. Installable as an app (PWA) and works offline.

## How to use

1. Sign in.
2. **Step 1 – mails.** In classic Outlook, open the folder where the group copies arrive and search `Shipment Arrival Notification`.
   Click one mail, press **Ctrl+A** then **Ctrl+C**, open **"Or paste the data instead"** and paste into the left box, then click **Use pasted data**.
   (An .xlsx / .csv exported from Access with *Subject* and *Received* columns also works as a file.)
3. **Step 2 – tracking list.** Load the Excel (.xlsx) with your AWBs. Only the sheet named **ALL NOA** is read (a .csv also works) (a column named *AWB* or *Tracking* is picked automatically).
4. Optionally set **Mails from / to** to check one bulk send, then press **Check**.
5. See **Missing / Shared / Extra / Sent more than once**, copy a list for Excel, or **Download Excel** with every list on its own sheet.

Rows are ignored when the **In Folder** column contains "Sent" (your Sent Items copy).

Dates are read as day/month/year (Bangladesh format). Times with no date, as Outlook shows for today's mails, count as today.

## Publish on GitHub Pages

1. Create a new repository on GitHub (e.g. `awb-mail-checker`).
2. Upload everything in this folder (keep the `icons` folder) to the repository root: **Add file → Upload files**, then commit.
3. Go to **Settings → Pages**, set **Source: Deploy from a branch**, branch **main**, folder **/ (root)**, and save.
4. After a minute the app is live at `https://<your-user>.github.io/awb-mail-checker/`.
5. Open that link in Chrome or Edge and press **Install app**. If the browser doesn't show its own prompt, the button explains why
   (opened as a file, missing files on GitHub, or a browser like Firefox) and shows the menu steps to install.

## Users and sign-in

Sign in with your **Email ID** (not case-sensitive) and password. Passwords are **not** stored in the files: `index.html` only
holds a salted PBKDF2-SHA256 hash for each user, checked in the browser.

**Add a user or change a password**
1. Open the app, press **F12** and go to **Console**.
2. Run `awbHash('name@bdexpress.com', 'NewPassword')`.
3. Copy the line it prints into the `USERS` list near the top of the script in `index.html`, removing that user's old line if any.
4. Raise `VERSION` in `sw.js` and upload both files.

**Remove a user:** delete their line from `USERS`.

> This sign-in only keeps casual visitors out. It runs in the browser, so it is not a server-side login, and a
> weak password could still be guessed offline from the hash. Use passwords that aren't used anywhere else, and
> prefer a private repository or the company intranet.

## Updating the app

After you change `index.html`, open `sw.js` and raise `VERSION` (e.g. `awb-checker-v2`) so installed copies pick up the new version.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app |
| `manifest.webmanifest` | App name, colours and icons for installing |
| `sw.js` | Offline cache |
| `icons/` | App icons |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |
