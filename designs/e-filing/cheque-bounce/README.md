# ON Courts — E-Filing (Cheque Bounce) prototype

The single-case e-filing wizard, unbundled from a one-file export into a proper
folder structure so it's legible, diff-able, and easy to build on or hand off.

## Structure

```
E-Filing-Cheque-Bounce/
  index.html      Launcher — links to every screen; open this first
  screens/        One HTML file per step (01 … 12), in flow order
  css/
    app.css       Shared styles
  js/
    runtime.js    Shared engine (React + the design-canvas runtime + design system + navigation)
  assets/         The document scans, as real image files
    aadhaar-card.jpg, aadhaar-card-back.jpg, cheque.png,
    return-memo.png, demand-notice.png, advocate-document.png
  README.md
```

Each screen in `screens/` is a standalone page that links `css/app.css` and
`js/runtime.js` and pulls its images from `assets/`. The screens link to each other
in order, so once one is open you can walk the whole flow.

## How to run it

This is a **served** project — the images and shared code are separate files, so
opening a screen by double-clicking (`file://`) will not render it. Run a tiny local
server from this folder instead:

```bash
cd E-Filing-Cheque-Bounce
python3 -m http.server 8000
```

Then open **http://localhost:8000** in a browser. (Any static server works — the
default entry is `index.html`, which every server looks for automatically.)

> Why not double-click? Browsers block one local file from loading another over
> `file://` for security. Splitting the monolith into real files is the right move for
> handoff and production; the small cost is that it now needs a server. Hosting it on
> GitHub Pages or Netlify serves it the same way, with a shareable URL.

## Handing it off

Zip the whole folder (not a single file) and tell the recipient to run the two
commands above, or push it to a repo and enable GitHub Pages. To swap a document,
replace the file in `assets/` with the same name — no code change needed.

## What changed from the single-file version

- The 12 screens were split into individual files under `screens/`.
- The embedded base64 scans were extracted into real image files in `assets/` (and
  de-duplicated — an image used on several screens now lives once).
- The shared runtime and styles were pulled out into `js/runtime.js` and
  `css/app.css`, so they exist once instead of being copied into every screen.
- In-flow navigation was repointed from the old single-file host to real page-to-page
  links between the `screens/` files.

## A note on the ceiling

This is a faithful **unbundling** of a design-tool export, not hand-authored
production code — the screens still render through the exported React/design-canvas
runtime. That's the right artefact for design review and handoff. Turning it into
clean, hand-written production HTML/CSS/JS is a separate rebuild, best done with
engineering.
