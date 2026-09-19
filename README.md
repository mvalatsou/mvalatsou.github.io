# marilina.valatsos.gr

Personal academic website, built with [Hugo](https://gohugo.io/).
Written from scratch in this repo (September 2026) — the older
`aethrvmn/marilina` repo was a copy of the *gokarna* theme with no content in it, so nothing was carried over except the two images.

---

## 1. Running the site on your laptop

Hugo is already installed (`hugo v0.152.2 extended`). If you ever need it on a new machine: `brew install hugo`.

```bash
cd ~/PhD/Repos/website
hugo serve
```

Then open **http://localhost:1313**. It rebuilds and refreshes the browser every time you save a file. `Ctrl-C` stops it.

To produce the final files for uploading:

```bash
hugo --gc --minify      # writes everything into public/
```

`public/` is gitignored — it is generated, never edit it by hand.

---

## 2. Where everything lives

```
hugo.toml                  ← site settings: name, tabs, photo, social links
content/                   ← THE TEXT OF THE SITE. This is what you edit most.
  _index.md                    home page
  about.md                     /about/
  research.md                  /research/
  cv.md                        /cv/
  publications.md              /publications/
  contact.md                   /contact/
data/
  publications.yaml        ← your paper list (see §4)
layouts/                   ← the HTML templates (the "theme"). Rarely touched.
  baseof.html                  the page skeleton every page is poured into
  home.html                    home page template (photo + name + text)
  page.html                    template for every normal page
  list.html                    template for a folder of pages
  404.html
  _partials/                   reusable bits: head, header, footer, icons/
  _shortcodes/                 custom markdown helpers (see §5)
assets/css/main.css        ← all styling. Colours are at the very top.
static/                    ← files served as-is
  images/                      self.png (portrait), logo.png (favicon)
  files/                       put cv.pdf here
archetypes/                template used by `hugo new`
```

**Rule of thumb:** the URL follows the filename.
`content/research.md` → `marilina.valatsos.gr/research/`.
A folder needs an `_index.md` inside it to have its own page; that is why the
home page is `content/_index.md`.

---

## 3. Everyday edits

### Change text on a page
Open the matching file in `content/` and edit the markdown.
Cheat sheet: <https://www.markdownguide.org/cheat-sheet/>

Every content file starts with a block between `+++` lines — the *front
matter*. Options used here:

| Key | Effect |
|---|---|
| `title` | heading of the page and the browser tab |
| `subtitle` | small grey line under the heading |
| `toc = true` | shows a "Contents" box built from the `##` headings |
| `math = true` | enables LaTeX on that page (`$...$` and `$$...$$`) |

### Add a new tab
1. Create `content/teaching.md` (or `hugo new content/teaching.md`).
2. Add a block to the `[menu]` section of `hugo.toml`:

```toml
[[menu.main]]
  name   = 'Teaching'
  url    = '/teaching/'
  weight = 7        # smaller number = further left
```

### Add your CV PDF
Drop it at `static/files/cv.pdf`. The download button on the CV page already
points there. *(It currently 404s because the file isn't there yet.)*

### Change the photo
Replace `static/images/self.png`, or point `avatar` in `hugo.toml` at a
different file. The favicon is `logo.png`, set by `logo`.

### Add an image to a page
Put it in `static/images/` and write `![Caption](/images/thing.png)`.

### Change colours
Top of `assets/css/main.css`, the `:root { … }` block. Light and dark palettes
are the same variable names redefined twice — edit both.

---

## 4. The publication list

Do **not** edit the Publications page markdown. Edit `data/publications.yaml`
and the page rebuilds itself, grouped by year, newest first:

```yaml
- title: "Exact title of the paper"
  authors: "A. Someone, **Marilina Valatsou**, B. Other"   # ** ** bolds your name
  venue: "Astronomy & Astrophysics, 690, A12"
  year: 2026
  type: article        # article | preprint | proceedings | thesis
  doi: "10.1051/0004-6361/xxxxx"
  arxiv: "2601.01234"
  note: "in review"    # optional, shown in the accent colour
```

Only `title`, `authors` and `year` are required. `doi`, `arxiv`, `url` and
`pdf` each become a small link button. Indentation matters in YAML — two
spaces, no tabs.

There are two placeholder entries in there right now; delete them.

---

## 5. Shortcodes (extra bits inside markdown)

| Shortcode | What it does |
|---|---|
| `{{< publications >}}` | renders `data/publications.yaml` |
| `{{< button href="/files/cv.pdf" blank="true" >}}Text{{< /button >}}` | pill button; add `style="ghost"` for the outlined version |
| `{{< cards >}}{{< card title="X" >}}text{{< /card >}}{{< /cards >}}` | responsive grid of boxes (used on Research) |

---

## 6. Other things that are already set up

- **Dark mode** — follows the system setting, plus the ☾/☀ switch in the
  header, remembered per browser. Turn the switch off with
  `themeToggle = false` in `hugo.toml`.
- **Mobile menu** — the tabs collapse into a burger menu under 640 px.
- **LaTeX** via KaTeX, loaded only on pages with `math = true`.
- **Social icons** in the footer come from `[[params.social]]` in
  `hugo.toml`. Available `icon` values: `email`, `github`, `gitlab`,
  `linkedin`, `orcid`, `scholar` (anything else falls back to a link icon).
  There is a commented-out ORCID entry ready to fill in.
- **RSS feed**, `robots.txt`, Open Graph tags for link previews.

---

## 7. Publishing to marilina.valatsos.gr

**Not set up yet — this still needs deciding.** The site currently only runs
locally. `baseURL` in `hugo.toml` is already the right domain. Where the DNS
for `marilina.valatsos.gr` currently points needs to be checked with Vasilis,
since the old repo had no deployment config in it.

The two easy options:

- **GitHub Pages** — push this repo to GitHub, add a workflow that runs
  `hugo --gc --minify` and publishes `public/`, then point a `CNAME` record
  for `marilina.valatsos.gr` at `<user>.github.io`.
- **Any web host / server** — run `hugo --gc --minify` and copy the contents
  of `public/` to the web root (e.g. with `rsync`). No server-side software
  is needed; it's plain static files.

---

## 8. Still to do

- [ ] Replace the placeholder text in `about.md`, `research.md`, `cv.md`,
      `contact.md` (office number, exact institute address).
- [ ] Put the real papers in `data/publications.yaml`.
- [ ] Add `static/files/cv.pdf`.
- [ ] Add ORCID / Google Scholar links in `hugo.toml`.
- [ ] Decide on hosting (§7).
