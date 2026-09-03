# evalvitals-pages

The EvalRx landing page. Live at
**https://evalvitals.github.io/evalvitals-pages/**

## Layout

    docs/                 generated; GitHub Pages serves from here
      index.html
      assets/fonts/       self-hosted .woff2 + OFL license texts
      site-src/            <- source, kept alongside the build it produces
        template.html      page markup, CSS, and (small, enhancement-only) JS
        build.py           assembles docs/index.html from template.html
        assets/fonts/      source fonts + OFL license texts

All content is server-rendered at build time — including the simulated-run
terminal in "What a full pass looks like" — so the page reads correctly with
JavaScript disabled. JS only staggers the terminal's reveal and handles the
scroll-in animation, copy buttons, and pixel avatars.

## Enable on GitHub Pages

1. Push `docs/` to the `main` branch.
2. In the GitHub repo: **Settings → Pages → Build and deployment → Source:
   "Deploy from a branch"**, then set **Branch: `main` / folder: `/docs`**.
3. GitHub publishes it at `https://evalvitals.github.io/evalvitals-pages/`.

No custom domain is configured. `evalvitals.com` is already bound to a
different repository (`xxlya/evalvitals-site`) — do not add a `CNAME` file
here without first confirming that domain should move.

## Editing the page

Edit `docs/site-src/template.html`, then rebuild:

```bash
python3 docs/site-src/build.py
cd docs && python3 -m http.server 8080
```

`docs/site-src/build.py` fills in the `<head>` (meta/OG/Twitter tags,
canonical URL, favicon), copies fonts + OFL licenses into `docs/assets/`,
renders the terminal walkthrough from the `TERM_LINES` list into real HTML,
and writes `docs/.nojekyll`, `docs/robots.txt`, and `docs/sitemap.xml`.

Content (thesis, loop diagram, repair ladder, comparison table, publications,
founders) is ported from the original `xxlya/evalvitals-site` landing page,
restyled to this repo's visual system (Fraunces + IBM Plex, the token/section
conventions used in
[`Nanboy-Ronan/RVCBench/docs`](https://github.com/Nanboy-Ronan/RVCBench/tree/main/docs)),
and corrected against the current package `README.md`/`docs/roadmap.md`
where the two had drifted — most notably, L4 (parameter-space repair) is now
marked **Built**: v1 executes LoRA fine-tuning on the language model from a
diagnosis-only pool, validated through the same paired McNemar + e-value
machinery as every other tier. Keep that cross-check in mind on future edits:
this page should track `evalvitals/evalvitals`'s actual shipped state, not
just its own history.
