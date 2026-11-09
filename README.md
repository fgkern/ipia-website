# IPIA Website

**GitHub repo:** https://github.com/fgkern/ipia-website  
**GitHub account:** fgkern  
**Local clone:** `/Users/florian/repos/ipia-website`  ← use this one

> **Two older copies exist under Dropbox. Do not edit either.**
>
> | Path | State |
> |------|-------|
> | `Dropbox/University of Essex/Admin/IPIA/Website/ipia-website` | Dead. Dropbox zeroed its `.git` internals, so git cannot open it. Nothing here can be committed or pushed. |
> | `Dropbox/Claude Code Flo/ipia-website` | Works, but was found 32 commits behind and sits in the same Dropbox hazard. Superseded by `~/repos/ipia-website`. |
>
> Once you are happy with `~/repos/ipia-website`, delete both to avoid editing the wrong one.

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
4. Commit and push normally:

   ```
   git commit -am "your message"
   git push
   ```

   A working token is stored in the macOS keychain, so plain `git push` just works —
   no token in the command, and no token written into `.git/config`.

5. Changes go live via GitHub Pages a minute or two after the push. Verify with
   `curl -s https://www.internationalpoliticsinafrica.org/events.html | grep ...`,
   and remember Pages takes a minute to rebuild.

### If a push suddenly fails with "Invalid username or token"

The stored token has expired. **The current one expires 2026-12-04.** Generate a new
fine-grained token at github.com/settings/tokens with **Contents: read and write** on
this repo, then re-store it:

```
printf 'protocol=https\nhost=github.com\n\n' | git credential-osxkeychain erase
printf 'protocol=https\nhost=github.com\nusername=fgkern\npassword=NEW_TOKEN\n\n' \
  | git credential-osxkeychain store
```

The same keychain entry serves `fgkern/future-essex-website`, so this fixes both repos.

## Events page

- Monthly virtual seminar (first Wednesday of the month).
- Seminars are listed in two sections: **Upcoming** and **Past**.
- When a seminar date has passed, move it from Upcoming to the top of Past — in all 4 language files.
- Language files: `events.html`, `fr/evenements.html`, `pt/eventos.html`, `sw/matukio.html`

## Language switcher

- "English" buttons on all pages must link to root-level pages (e.g. `/events.html`), never to `/en/`.

## The stale-clone guard

A `pre-commit` hook in `.githooks/` fetches from GitHub and **blocks the commit** if this
clone is behind, rather than letting you build on an out-of-date copy. It is enabled with:

```
git config core.hooksPath .githooks
```

That setting is per-clone and is **not** carried over by `git clone`, so run it once in any
fresh clone. If GitHub is unreachable the hook warns and lets the commit through; for a
deliberate offline commit use `SKIP_STALE_CHECK=1 git commit ...`.

## Why this repo is no longer in Dropbox

Dropbox and git do not get along. Git keeps its bookkeeping in many small files under `.git`,
and Dropbox syncs them individually, which can catch them mid-write. The old
`University of Essex/Admin/...` clone died exactly this way — its `.git/HEAD` and
`.git/config` are now 0 bytes, so git refuses to open it and nothing in it can be pushed.

Keep this repo at `~/repos/ipia-website`, outside any synced folder. If git ever reports
"not a git repository" in a clone that used to work, this is the likely cause; re-clone
from GitHub.

## Hosting (GitHub Pages)

- Served by GitHub Pages, "deploy from branch": `main` / root, custom domain `www.internationalpoliticsinafrica.org` (see `CNAME`). No Actions workflow.
- **Making the repo private turns Pages off, and making it public again does not turn it back on.** If the site goes down after a visibility change, go to Settings → Pages and set the source to `main` / `(root)` with the custom domain, or run:
  ```
  gh api -X POST repos/fgkern/ipia-website/pages -f "source[branch]=main" -f "source[path]=/"
  gh api -X PUT  repos/fgkern/ipia-website/pages -f cname=www.internationalpoliticsinafrica.org
  ```
  (Done on 2026-11-06 after the site went down.)
