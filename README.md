# IPIA Website

**GitHub repo:** https://github.com/fgkern/ipia-website  
**GitHub account:** fgkern (authenticated via `gh` CLI)  
**Local clone:** `/Users/florian/Dropbox/University of Essex/Admin/IPIA/Website/ipia-website`

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

1. Edit the relevant root-level file(s) for English content.
2. Apply the equivalent change to `fr/`, `pt/`, and `sw/` versions.
3. Commit and push: `git push` (GitHub auth is via `gh` CLI keyring, no token needed).

## Events page

- Monthly virtual seminar (first Wednesday of the month).
- Seminars are listed in two sections: **Upcoming** and **Past**.
- When a seminar date has passed, move it from Upcoming to the top of Past — in all 4 language files.
- Language files: `events.html`, `fr/evenements.html`, `pt/eventos.html`, `sw/matukio.html`

## Language switcher

- "English" buttons on all pages must link to root-level pages (e.g. `/events.html`), never to `/en/`.
