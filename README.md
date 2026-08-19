# Deep Time Earth — v1.0

Coastlines, ice sheets and climate zones for the next 400,000 years. One self-contained
HTML file: no server, no build step, no external requests. Open it and it runs.

## What's in this folder

| File | Size | |
|---|---|---|
| `index.html` | 7.1 MB (5.1 MB over the wire) | 2160 × 1080 terrain. **Share this one.** Loads in a second or two on almost anything, including phones on mobile data. |
| `full.html` | 21.8 MB (16 MB over the wire) | 4320 × 2160 terrain. Visibly sharper when you zoom into a mountain range; a long wait on a slow connection. |
| `.nojekyll` | 0 B | Tells GitHub Pages not to run its Jekyll pre-processor over the folder. Harmless everywhere else. |

Both files are byte-identical apart from the terrain payload.

## Putting it on the web

Any static host works — there is nothing to configure, no environment variables, no
secrets in the file. Three that are free and take about two minutes:

### Netlify Drop — fastest, no account needed to start
1. Go to <https://app.netlify.com/drop>
2. Drag this whole `dist` folder onto the page.
3. You get a URL immediately, something like `random-name-123.netlify.app`.
4. Make a free account if you want to keep it and rename it to something sensible.

### GitHub Pages — most durable, good if you already have an account
1. Make a new public repository.
2. Upload the contents of this folder to it (drag them onto the repo page in the browser — no git needed).
3. Settings → Pages → Source: *Deploy from a branch* → `main` / `/ (root)` → Save.
4. A minute later it's at `https://<your-username>.github.io/<repo-name>/`.

Limits are generous: 1 GB site, 100 GB/month bandwidth, files up to 100 MB.

### Cloudflare Pages — fastest delivery
1. <https://pages.cloudflare.com> → Create a project → *Direct Upload*.
2. Drag the folder in.

One caveat: Cloudflare Pages caps a single file at **25 MiB**. `full.html` is 20.8 MiB,
so it fits, but not by much — if you ever regenerate it at higher resolution it will
stop deploying there.

## Things worth knowing before you share it

- **It's all client-side.** The file makes no network requests once loaded and stores
  nothing. Nobody's data goes anywhere.
- **It needs WebGL2**, which every browser from the last several years has. On a very
  old device it will say so rather than showing a blank page.
- **First load does real work.** It unpacks the terrain, works out the snowlines, and
  builds a derived climate series — about two to four seconds on a laptop, with a
  progress bar. After that it is smooth.
- **Phones work.** One finger pans, two fingers pinch to zoom, and the panel stacks
  under the map.

## What it is

A small climate model — orbit, carbon, ice, sea level, rainfall — driving a WebGL map,
built and then reviewed hard over nine rounds. It reproduces two of the four dated
glacial terminations of the last 400,000 years from dates it was never fitted to, puts
the drawn glacial ice within 0.1 m of the sea level its own curve claims, and scores
1.96 °C mean error against 105 climate stations.

It also gets plenty wrong, and says so: open the **About this app** section in the
panel for what is left out and how much to trust the dates.
