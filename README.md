# 360° Panorama Viewer & Tour Builder

Two self-contained, single-file web apps for viewing and sharing 360° (equirectangular) images. No server, no build step, no account — everything runs in the browser, and all data travels in the share link itself.

| App | File | Open it |
|---|---|---|
| **360 Viewer** — view and share a single panorama | [`360.html`](360.html) | [Launch ▶](360.html) |
| **Orbit Tour Builder** — link multiple panoramas into a virtual tour | [`tour.html`](tour.html) | [Launch ▶](tour.html) |

> Replace `USERNAME` and `REPO` above with your GitHub username and repository name, and enable **GitHub Pages** (Settings → Pages → deploy from the main branch) so the "Launch" links work.

---

## 360.html — 360° Image Viewer

A minimal viewer for a single spherical image.

### How to use

1. Open `360.html` in your browser (via the link above).
2. Paste a **direct URL** to an equirectangular image (ends in `.jpg`/`.png`) into the top bar and click **Load** — or click **Try a sample panorama**.
3. Look around:
   - **Drag** to pan
   - **Scroll / pinch** to zoom (field of view 30–100°)
   - **Arrow keys** to pan, **+ / −** to zoom
4. A compass strip along the bottom tracks your heading; the toolbar auto-hides while you're viewing.
5. Click **Share** to copy a link (`?img=...`) that opens directly into the same panorama.

## tour.html — Orbit Tour Builder

Builds multi-scene virtual tours: load several 360° images, drop markers on them, and link markers from one scene to another. The entire tour — image URLs, scene names, markers, captions, and descriptions — is compressed into the share link's URL hash (`#t=...`), so anyone with the link sees the full tour.

### How to use

1. Open `tour.html` and paste a 360° image URL into the top bar, then click **Load**. This becomes your first scene.
2. Open the **Tour** panel (bottom-left) to manage scenes:
   - Add more scenes with the **New scene image URL** field
   - Click a scene to switch to it; rename or delete scenes from the list
3. Add markers: click **＋ Place a marker**, then click anywhere on the panorama. Each marker can have:
   - A **title** (up to 140 characters)
   - A **description** (up to 200 characters)
   - An optional **link to another scene** — linked markers show an amber arrow, and clicking one offers a "Go to [scene]" button, which is how viewers walk through the tour
4. The **sun icon** toggles auto brightness/contrast enhancement (computed per scene on the GPU); the setting is saved into the share link.
5. Click **Share tour** to copy a link containing the whole tour. Opening it rebuilds everything — no server or storage involved.
6. On a VR-capable device over HTTPS, a **VR button** appears for immersive WebXR viewing.

---

## Requirements & tips

- **Image URLs must allow CORS.** The apps render with WebGL, which needs pixel access, so the image host must permit cross-origin requests. Direct links from Wikimedia Commons and most CDNs work; sites that block embedding won't, and the app shows an error explaining this.
- **Serve over HTTPS** for full functionality. Opening the files from disk (`file://`) still renders panoramas, but the clipboard-based Share and the VR mode require a secure context. GitHub Pages provides HTTPS automatically.
- **Long links are normal.** Because the tour data lives in the URL, large tours (many scenes and fully written descriptions) produce long links. Typical 5–10 scene tours are fine, but some older systems truncate URLs past ~2,000 characters, so test wherever you plan to share.
- **Dependencies:** each file loads Three.js (and, for the tour builder, lz-string) from cdnjs.cloudflare.com. For a fully offline deployment, download those scripts and point the `<script>` tags at local copies — that's the only change needed.
- Images can be hosted anywhere with CORS headers; they don't need to live in this repository.

## Where to find 360° images

Any equirectangular (2:1 spherical) image works — photos from a 360° camera, exports from Google Street View tools, or free samples from Wikimedia Commons and Flickr (search "equirectangular").
