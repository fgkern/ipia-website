# IPIA Website

**GitHub repo:** https://github.com/fgkern/ipia-website  
**GitHub account:** fgkern  
**Local clone:** `/Users/florian/Dropbox/Claude Code Flo/ipia-website`

> **Do not use** `/Users/florian/Dropbox/University of Essex/Admin/IPIA/Website/ipia-website`.
> That folder looks like a clone and still holds a full set of site files, but Dropbox has
> emptied its `.git` internals to 0 bytes, so git refuses to open it. Any edits made there
> cannot be committed or pushed. Treat it as dead and edit only the path above.

## Structure

The site is static HTML/CSS. The real English pages live at the **root level**:

| File | Page |
|------|------|
| `index.html` | Home / About IPIA |
| `about.html` | About |
| `leadership.html` | Leadership and Steering Committee |
| `writing-workshop.html` | Writing Workshop |
| `workshop-programme.html` | Workshop Programme |
| `events.html` | Events |

Language versions are in subdirectories:

| Folder | Language |
|--------|----------|
| `fr/` | Français |
| `pt/` | Português |
| `sw/` | Kiswahili |

> The `en/` directory is an old placeholder — ignore it.

## Making changes

1. **Fetch first — always:** `git fetch origin && git status`

   `git status` on its own will happily report "up to date" while the clone is dozens of
   commits behind, because it compares against the last copy of the remote it downloaded
   rather than against GitHub. Without a fetch you can end up editing a months-old version
   of a page and overwriting newer work. Fetching refreshes that copy so the comparison is real.

2. Edit the relevant root-level file(s) for English content.
3. Apply the equivalent change to `fr/`, `pt/`, and `sw/` versions.
4. Commit, then push with a fine-grained personal access token:

   ```
   git push "https://x-access-token:YOUR_TOKEN@github.com/fgkern/ipia-website.git" main
   ```

   The `gh` CLI is **not** installed on this machine and the saved macOS keychain credential
   no longer works ("Invalid username or token"), so a plain `git push` will fail. Generate a
   token at github.com/settings/tokens with **Contents: read and write** on this repo.
   Installing `gh` (`brew install gh` then `gh auth login`) would remove the need for tokens.

5. Changes go live via GitHub Pages a minute or two after the push.

## Events page

- Monthly virtual seminar (first Wednesday of the month).
- Seminars are listed in two sections: **Upcoming** and **Past**.
- When a seminar date has passed, move it from Upcoming to the top of Past — in all 4 language files.
- Language files: `events.html`, `fr/evenements.html`, `pt/eventos.html`, `sw/matukio.html`

## Language switcher

- "English" buttons on all pages must link to root-level pages (e.g. `/events.html`), never to `/en/`.

## A caution about Dropbox

This repo lives inside a Dropbox folder. Dropbox and git do not get along: Dropbox syncs the
hidden `.git` directory file by file, and can corrupt it mid-write. That is exactly what
happened to the dead clone noted at the top — its `.git/HEAD` and `.git/config` are now empty
files. If git ever starts reporting "not a git repository" here, that is the likely cause; the
fix is to re-clone from GitHub, ideally to a location outside Dropbox.
