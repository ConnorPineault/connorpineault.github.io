# connorpineault.github.io

Personal website. Plain HTML and CSS — no build step, no dependencies.

## Files

| File | What it is |
|---|---|
| `index.html` | Landing splash — name and contact, centered. Clicking the name enters the site |
| `about.html` | About page and contact details |
| `resume.html` | Education, experience, skills |
| `projects.html` | Side projects |
| `publications.html` | Publications, including work in preparation |
| `style.css` | All styling |
| `assets/connor.jpg` | Headshot, 400×400 |
| `.nojekyll` | Stops GitHub from running Jekyll over the files |

## Editing

Open the `.html` file, change the text, save. There is nothing to compile.

Colors, fonts, and spacing all live in the `:root` block at the top of `style.css`.
The site commits to a single beige-and-black look — there is no dark mode.

## Preview locally

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Deploy

The repo must be named exactly `connorpineault.github.io` to serve from the root URL.

```sh
gh repo create connorpineault.github.io --public --source=. --push
```

Then: repo Settings → Pages → Source → `main` / root. Live in about a minute at
<https://connorpineault.github.io>.

After that, every `git push` to `main` redeploys.

## Regenerating the resume PDF

`assets/Connor-Pineault-Resume.pdf` is generated from `resume.html`, not maintained by
hand — so the download can never drift from what the page says. The `@media print`
block in `style.css` controls how it lays out: it hides the nav and download link,
shows a print-only name-and-contact header, and tightens spacing to fit one page.

After editing `resume.html`, serve the site and re-render:

```sh
python3 -m http.server 8000 &
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless=new --disable-gpu --no-pdf-header-footer \
  --print-to-pdf="$PWD/assets/Connor-Pineault-Resume.pdf" \
  http://localhost:8000/resume.html
```

Check it still fits on one page. If it spills, tighten the margins in the `@media print`
block rather than cutting content.

## Not done yet

- **Publications page.** Lists one manuscript in preparation. Add real citations, and a
  "Published" section above it, once papers land.
