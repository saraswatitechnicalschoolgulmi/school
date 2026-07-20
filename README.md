# Link Fix Package — Shree Saraswati Secondary School Website

This package contains the fixed files from the audit of
https://github.com/saraswatitechnicalschoolgulmi/school

## What to do
Copy these files into your repo at the SAME paths, overwriting the existing ones:

- `index.html`            → replaces root `index.html`
- `html/index.html`       → replaces `html/index.html`
- `images/img.png`        → NEW file (fallback image)
- `images/img1.jpg`       → NEW file (fallback image)
- `images/img2.jpg`       → NEW file (fallback image)
- `images/img3.jpg`       → NEW file (fallback image)

Then commit and push, e.g.:

```
git add index.html html/index.html images/img.png images/img1.jpg images/img2.jpg images/img3.jpg
git commit -m "Fix broken About Us links, favicon path, and add image fallback files"
git push
```

Alternatively, apply `changes.patch` with:

```
git apply changes.patch
```
(Note: the patch only covers the two edited HTML files — you'll still need to
manually add the 4 new image files listed above, since they're new binary files.)

## What was fixed

1. **index.html (root) — broken "About Us" dropdown links**
   - Before: `about.html#history`, `about.html#campuses`, `about.html#team`
     (pointed to a non-existent root-level about.html)
   - After: `html/about.html#history`, `html/about.html#campuses`, `html/about.html#team`

2. **html/index.html — broken favicon**
   - Before: `<link rel="icon" ... href="images/logo.png" />` (resolves to a
     non-existent html/images/ folder)
   - After: `<link rel="icon" ... href="../images/logo.png" />`

3. **Missing image fallback files**
   - Several `<img>` tags use `onerror` to fall back to an alternate file
     extension (e.g. img1.png → img1.jpg) that didn't exist on disk.
   - Added img.png, img1.jpg, img2.jpg, img3.jpg as copies of their
     existing counterparts so the fallback never 404s.

## Not changed (kept as-is per your instruction)

- `html/index.html` is an older/different-styled duplicate of the homepage
  and isn't linked from anywhere in the site nav. You said you use it for
  something, so it was left in place — only its favicon path was fixed.
- `student-login.html`, `organizational-tree.html`,
  `staff-management-admin.html`, and `faculty-showcase.html` are not linked
  from any nav menu (they appear to be standalone tools opened directly by
  URL). No changes made — flagging in case that's not intentional.

## Full audit result

Every `href`/`src` across `index.html`, `html/*.html`, and `js/*.js` was
crawled and checked against the actual file tree. Aside from the items
above, all links, images, CSS, and JS references resolve correctly.
