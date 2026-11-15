# Cantonese Flashcards (iPhone web app)

A version of the flashcards app that runs entirely in the browser, with no server and no audio.
Each card shows the Jyutping and you type the Traditional characters or an English definition.

## What's in this folder

| File | What it is |
|---|---|
| `index.html` | The app |
| `cards.js` | Your word list, generated from MASTER.xlsx |
| `build_cards.py` | Rebuilds `cards.js` from MASTER.xlsx (run on your computer) |
| `sw.js`, `manifest.webmanifest`, `icon-180.png`, `icon-512.png` | Make it work offline and look like an app on the Home Screen |

`build_cards.py` and this README don't need to be uploaded, but it does no harm if they are.
**Don't upload MASTER.xlsx.**

---

## One-time setup on GitHub (about 10 minutes, no Git needed)

1. **Make an account** at <https://github.com> if you don't have one.
2. **Create a repository.** Click **+** (top right) → **New repository**.
   - Name it something like `canto-cards`.
   - Choose **Public**. Free GitHub accounts can only publish public repositories as websites,
     so anyone who finds the link can see the word list.
   - Click **Create repository**.
3. **Upload the files.** On the new repository's page, click **uploading an existing file**
   (or **Add file → Upload files**). Drag in `index.html`, `cards.js`, `sw.js`,
   `manifest.webmanifest`, `icon-180.png` and `icon-512.png`, then click **Commit changes**.
4. **Turn on GitHub Pages.** Go to **Settings → Pages**. Under **Build and deployment**, set
   **Source** to **Deploy from a branch**, **Branch** to **main** and the folder to **/ (root)**, then click **Save**.
5. **Wait a minute or two**, then refresh that Settings → Pages screen. It will show your address,
   like `https://YOUR-USERNAME.github.io/canto-cards/`.

## Put it on your iPhone

1. Open that address in **Safari**. (Other iPhone browsers can't add web apps to the Home Screen properly.)
2. Tap the **Share** button → **Add to Home Screen** → **Add**.
3. **Always study from the Home Screen icon**, not from a Safari tab. Saved progress isn't shared
   between the two, and progress in the Home Screen app is safe from Safari's automatic clean-up.
4. After you've opened it once, it also works offline.

> Deleting the Home Screen icon deletes its saved progress. Export a backup first (see below).

## Updating the word list after you edit MASTER.xlsx

1. On your computer, put `build_cards.py` in the same folder as MASTER.xlsx and run:
   ```
   pip install openpyxl
   python build_cards.py
   ```
   (Or `python build_cards.py path/to/MASTER.xlsx`.) It writes a new `cards.js` next to the script.
2. On GitHub, open your repository → **Add file → Upload files** → drag in the new `cards.js` → **Commit changes**.
   It replaces the old one.
3. Wait a minute or two, then open the app on your phone while you're online. It picks up the new list automatically.
   If it doesn't, close the app fully (swipe it away) and open it again.

Your progress is kept across updates. Progress is saved per word, so editing a definition doesn't reset it.
If a word was in a half-finished session and you delete it from the spreadsheet,
that saved session can't be resumed, but the rest of your history is kept.

## Backing up and moving progress

In the app, under **Progress backup**:
- **Export progress** opens the iPhone share sheet. Choose **Save to Files** (e.g. iCloud Drive).
- **Import progress** loads a backup file and replaces this device's progress.

The import also accepts the `progress.json` from the old Python version,
so you can carry over which words you'd already learned.

## What changed from the Python version

- Removed: audio, the Phonetic column, the local server, and the "Reload spreadsheet" button.
- New: a **Prompt** setting to show iPhone modified Jyutping (default), modified Jyutping or standard Jyutping.
  Standard Jyutping is still shown after each answer.
- New: export/import of progress.
- Words that appear on more than one row in the spreadsheet are tracked separately.
  For those words, an English answer counts if it matches any of their definitions.
- Everything else (settings, grading rules, rounds, overrides, resume, "skip learned words") works as before.
