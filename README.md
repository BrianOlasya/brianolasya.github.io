# Portfolio — Nickson Brian Olasya

Static one-page portfolio. No build step, no dependencies, no framework.
Total size ≈ 11 MB (88 images, the icon set and one HTML file).

```
index.html          the entire site — HTML, CSS and JS in one file
img/                88 photographs, 1200–1600 px max edge, ~76–84% JPEG quality
img-manifest.json   maps each image back to its source file in the archive
favicon.ico         browser tab icon (16/32/48 px, gold B monogram)
favicon-16x16.png   \
favicon-32x32.png    | modern browsers prefer these over the .ico
apple-touch-icon.png  home-screen icon for iOS (180 px)
icon-192.png        \
icon-512.png         | Android / installed-app icons, referenced by the manifest
site.webmanifest    name, colours and icons for when the site is saved to a home screen
.nojekyll           tells GitHub Pages to serve the folder as-is
```

## Contact links

Contact links are already filled in. If you ever need to change them, search `index.html` for `linkedin.com` and `github.com`:

```html
<a class="cta" id="li" href="https://www.linkedin.com/in/brian-olasya/">
<a class="cta" id="gh" href="https://github.com/BrianOlasya?tab=repositories">
```

Everything else is ready to publish as-is.

## Deploying to GitHub Pages

The site is configured for **`https://brianolasya.github.io`**. The repository must be
named exactly `brianolasya.github.io` and be public.

> **Publish this folder only — never its parent.** `MyPortfolio/` also contains the
> `Engineering/` archive, which holds invoices, a business permit, budget whiteboards and a
> photograph of a spreadsheet with plaintext passwords. Running `git init` one level up would
> put all of it on the public internet. Run the commands below from inside `portfolio-site/`,
> and check `git status` lists only site files before the first commit.

```bash
cd portfolio-site
git init
git add .
git status                     # expect ~100 files, all site assets, nothing from Engineering/
git commit -m "Portfolio"
git branch -M main
git remote add origin https://github.com/BrianOlasya/brianolasya.github.io.git
git push -u origin main
```

Then: Settings → Pages → Source *Deploy from a branch*, Branch `main`, Folder `/ (root)`.
Live in 1–2 minutes.

### After the first deploy

Paste the URL into the [LinkedIn Post Inspector](https://www.linkedin.com/post-inspector/)
once. It shows what the link preview will look like and forces LinkedIn to re-scrape — LinkedIn
caches previews for around a week, so if the first scrape happens before the site is live, the
broken version sticks around.

## Custom domain, later

Four URLs in `index.html` hardcode `https://brianolasya.github.io` — `og:url`, `og:image`,
`twitter:image` and `<link rel="canonical">`. They are grouped together in the `<head>` under a
comment. To move:

1. Buy the domain.
2. Find-and-replace `https://brianolasya.github.io` with `https://<new-domain>` in `index.html`.
3. Add a file named `CNAME` (no extension) to this folder containing just the bare domain,
   e.g. `nicksonolasya.com` — no `https://`, no trailing slash.
4. At the registrar: four `A` records for the apex → `185.199.108.153`, `185.199.109.153`,
   `185.199.110.153`, `185.199.111.153`, and a `CNAME` for `www` → `brianolasya.github.io`.
5. Settings → Pages → Custom domain: enter it, then tick **Enforce HTTPS** once the certificate
   is issued (usually under an hour).

GitHub keeps redirecting `brianolasya.github.io` to the new domain afterwards, so links already
shared keep working.

## Editing the content

Everything is in `index.html`, in reading order — hero, spectrum, projects, earlier work, register, capabilities, experience, recognition, contact.

- **A project's photos** live in the `<div class="shots">` block for that project. Delete a `<figure>` to drop an image; the grid reflows on its own.
- **The full register** is the `REG` array in the `<script>` at the bottom: `["Name", file count, "N days", "years"]`.
- **Colours and type** are CSS custom properties in the `:root` block at the top. `--hot` is the orange accent; change it there and it changes everywhere.

## The icon

All icon files are generated from the gold **B** monogram. To change it, replace the
artwork and regenerate every size — `favicon.ico` (16/32/48), `favicon-16x16.png`,
`favicon-32x32.png`, `apple-touch-icon.png` (180), `icon-192.png`, `icon-512.png` —
keeping the same filenames, so no HTML has to change. The small sizes are sharpened
slightly; a straight downscale of a fine-line monogram goes muddy at 16 px.

## Notes

- The design is deliberately single-theme (dark). Photographs of workshop work read better against it, and it avoids the light/dark inconsistencies that come from theming a photo-led page.
- Images are lazy-loaded; the lightbox is keyboard-accessible (Enter to open, arrows to move, Escape to close).
- Fonts come from Google Fonts — the only external request the page makes. If you ever need the site to work fully offline, download the three families and swap the `<link>` for local `@font-face` rules.

## Replacing or adding images

Source images live in the archive under `Engineering/<NN Thread Name>/`. To add one:

1. Resize the longest edge to 1200 px, save as JPEG quality ~76.
2. Drop it in `img/` with a descriptive lowercase-hyphen name.
3. Add a `<figure class="shot">` block to the relevant project, copying an existing one.

`img-manifest.json` records which archive file each current image came from, so you can always find the original at full resolution.
