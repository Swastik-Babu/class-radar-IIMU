[README-classradar-setup.md](https://github.com/user-attachments/files/29610547/README-classradar-setup.md)
# ClassRadar Setup — Private Sheet via Google Sign-In

Your sheet stays exactly as private as it is now. Instead of making it
public, you sign into the app with your own Google account (the one that
already has access to the sheet), and the app reads it on your behalf.

This requires the app to be hosted at a real `https://` address — Google's
sign-in system won't work if you just open the HTML file directly on your
phone. GitHub Pages gets you a free, permanent link in a few minutes.

## Part A — Host the file (GitHub Pages)

1. Go to https://github.com and create a free account if you don't have one.
2. Click **+ → New repository**. Name it anything, e.g. `classradar`. Set it
   to **Public**. Create it.
3. In the new repo, click **Add file → Upload files**, upload `classradar.html`,
   but **rename it to `index.html`** during upload (click the filename to edit it).
4. Commit the upload.
5. Go to the repo's **Settings → Pages**. Under "Source," choose **Deploy from
   a branch**, branch = `main`, folder = `/ (root)`. Save.
6. Wait ~1 minute, then refresh — GitHub shows your live URL, something like:
   `https://YOUR_USERNAME.github.io/classradar/`

Keep that URL — it's your app's permanent address. Bookmark it, and later
"Add to Home Screen" on it from your phone.

## Part B — Google Cloud setup (OAuth)

1. Go to https://console.cloud.google.com and create a new project (or reuse
   one if you already made one for this).
2. **APIs & Services → Library** → search "Google Sheets API" → **Enable**.
3. **APIs & Services → OAuth consent screen**:
   - User type: **External**
   - Fill in app name (e.g. "ClassRadar"), your email for support/contact.
   - Scopes: click **Add or Remove Scopes**, search for and add
     `.../auth/spreadsheets.readonly`. Save.
   - Test users: add your own Google email address here. (While the app is
     in "Testing" mode, only accounts listed here can sign in — that's fine,
     it's just you.)
4. **APIs & Services → Credentials → Create Credentials → OAuth client ID**:
   - Application type: **Web application**
   - Name: anything
   - **Authorized JavaScript origins** → Add URI → paste your GitHub Pages
     origin **without a trailing path**, e.g. `https://YOUR_USERNAME.github.io`
   - Create. Copy the **Client ID** shown (ends in `.apps.googleusercontent.com`).

## Part C — Share the sheet with your own account (if not already)

If the sheet is a college sheet shared with your account (e.g. your college
email has view access), you're already set — just make sure you sign into
the app with that same Google account.

## Part D — Configure the app

1. Open your GitHub Pages URL on your phone.
2. Fill in:
   - **Spreadsheet ID** — from the sheet's URL
   - **Tab name** — e.g. `Term-IV`
   - **Google OAuth Client ID** — from Part B step 4
   - Your courses/sections (pre-filled already, edit if needed)
3. Tap **Sign in with Google & continue**, choose your college account,
   approve the permission (read-only access to Sheets).
4. Done — it'll test the connection and drop you into the main screen.

## Notes

- Sign-in tokens expire after about an hour. The app tries to silently
  refresh in the background; if that's not possible (e.g. you closed the
  browser fully), you'll see a small "Sign in" banner — one tap and you're
  back in.
- Because "Testing" mode OAuth apps in Google Cloud only allow the test
  users you listed, this is effectively locked to just your account unless
  you explicitly add others in the OAuth consent screen settings.
- If you ever change the sheet's tab name (new term), update it from the
  app's settings (⚙ icon, top right).
