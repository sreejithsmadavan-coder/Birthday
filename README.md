# Rithudev's first birthday — invitation site

Upload every file in this folder to the same directory on your host. Nothing else is needed;
the photo is embedded inside `index.html`, so there are no image paths that can break.

```
index.html              the invitation
img/rithudev.jpg        the graded portrait used in the invitation
og-cover.jpg            the sealed envelope shown in the WhatsApp preview (1200x630)
og-cover-square.jpg     square version, for Instagram or WhatsApp Status
favicon.svg             browser tab icon
apple-touch-icon.png    icon if a guest saves it to their home screen
.vscode/                editor settings and a Live Server recommendation
```

## Opening it in VS Code

Open this whole folder (File -> Open Folder), not just `index.html`. VS Code will offer to
install Live Server; accept it, then right-click `index.html` and choose **Open with Live
Server**. It serves the folder at `http://127.0.0.1:5500` and reloads the browser every time
you save.

Do not open `index.html` by double-clicking it in your file manager. It mostly works, but the
page is served over `file://`, and some things behave differently there than they will on your
real host.

## The one edit you must make

Open `index.html` and find this block near the top:

```html
<meta property="og:image" content="https://YOUR-DOMAIN/og-cover.jpg">
<meta property="og:url"   content="https://YOUR-DOMAIN/">
```

Replace `YOUR-DOMAIN` with the real address, in **both** lines. For example, if the invitation
lives at `https://rithudev.webc.in/`, they become:

```html
<meta property="og:image" content="https://rithudev.webc.in/og-cover.jpg">
<meta property="og:url"   content="https://rithudev.webc.in/">
```

These must be full absolute URLs starting with `https://`. Relative paths like `/og-cover.jpg`
will not work — WhatsApp fetches the image from its own servers and has no idea what your
domain is.

## Before you send it to anyone

1. Open the URL on your own phone and check the invitation opens and scrolls correctly.
2. Send the link to yourself on WhatsApp first. Wait for the envelope preview to appear
   **before** hitting send.
3. Tap through: preview -> page loads -> tap the seal -> invitation unfolds.
4. Tap "Get directions" and confirm the map lands at the auditorium.

## If the preview does not appear

WhatsApp caches link previews hard, and it caches failures too. If you share the link even
once before the meta tags are correct, it will keep showing nothing for hours.

- Make sure `YOUR-DOMAIN` was replaced and the page is live before the first share.
- Confirm the image loads on its own: open `https://your-domain/og-cover.jpg` in a browser.
- The site must be `https`. WhatsApp will not fetch previews over plain `http`.
- To break a stuck cache, share `https://your-domain/?v=2` instead. Change the number each
  time you need a fresh fetch.
- To check what the crawlers actually see, paste the URL into
  <https://developers.facebook.com/tools/debug/> and press "Scrape Again". WhatsApp uses the
  same crawler as Facebook.

## Hosting options

**Your own server.** Upload the folder over FTP or cPanel. Simplest if you already have
hosting.

**Netlify Drop** — <https://app.netlify.com/drop>. Drag this whole folder onto the page and
you get a live https URL in about ten seconds, free, no account needed to start. You can
attach your own domain later.

**Cloudflare Pages** or **GitHub Pages** both work the same way and are free.

## Changing the wording later

All the text lives in one `INVITE` block near the top of `index.html` — names, date, venue,
the map link, the sign-off. Edit those values and re-upload. Nothing else in the file needs
to be touched.
