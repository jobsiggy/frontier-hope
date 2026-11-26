# Frontier Signal

A responsive, offline-capable, single-file web app for organizing **public** frontier-AI signals, viewing transparent theme clusters, and creating evidence-grounded prompts for Arena AI Agent Mode.

The product treats RSS items, public posts, research/news updates, and open roles as **clues to verify**, not proof of a lab's private work or a forecast. Built-in starter records are fictional and visibly labeled as demo data.

## Run it

No build step, package manager, API key, or backend is required.

- Open `index.html` directly in a modern browser for the offline demo.
- Or serve the repository root locally:

  ```sh
  python3 -m http.server 8000 --bind 0.0.0.0
  ```

  Then visit `http://localhost:8000`.

The app uses vanilla HTML, CSS, and JavaScript and has no external runtime dependencies. Layouts adapt for desktop, tablet, and mobile; reduced-motion preferences are respected.

## What it does

- **Signal desk:** overview metrics, an animated interface, a weekly activity chart, recurring focus areas, and recent items.
- **Evidence signals:** search and filter by text, source type, topic, and organization; open original URLs; pin real imported records to a prompt; remove local records.
- **Frontier map:** group signal text into visible, keyword-based themes (agents and tools, model efficiency, multimodal, infrastructure, safety and alignment, robotics, and data and training). Coverage labels describe record count and source mix only; they are not confidence scores or predictions.
- **Sources & intake:** fetch a public RSS / Atom URL where the publisher permits browser CORS, enter public social posts manually, or paste/import RSS/Atom XML, JSON, or CSV.
- **Arena prompt studio:** a 10-step brief builder that adds a user-imported evidence snapshot, exports Markdown or JSON, and creates an Arena Agent Mode prompt for the user to review and paste.
- **Eval & rubric tools:** generate a weighted Markdown rubric with 1–5 anchors and a self-contained evaluation spec.
- **Quality checker:** heuristic checks for explicit goals, deliverables, pass criteria, evidence rules, boundaries, recovery guidance, phases, and output contract. Its score is not a quality guarantee.
- **Best-of-N pack:** prepare 2–5 copies for separate Arena chats. It does not run chats or select models.
- **Help & how to:** in-app operating, evidence, privacy, and limitation guidance.

## Add public evidence

### RSS / Atom URL

Go to **Sources & intake**, enter an `http://` or `https://` feed URL, and choose **Fetch public feed**. The app fetches directly from your browser. A publisher may block this with CORS; this is expected for some feeds. If so, download or copy the public feed and use the local import controls instead. There is no proxy or automated polling.

### Paste or import a file

Accepted input:

- RSS or Atom XML with `<item>` or `<entry>` records.
- A JSON array, or an object containing an `items`, `entries`, `signals`, or `data` array.
- CSV with a `title` or `name` column. Optional fields can include `summary`, `description`, `organization`, `kind`, `topic`, `published`, and `url`.

File contents are parsed in the browser. Markup in excerpts is treated as text; embedded scripts are not executed.

### Public social post

Paste text you can publicly access, its organization, publication date, platform/source type, and preferably the direct public URL. Posts are entered manually; the app does not sign in, crawl accounts, or post content back to a service.

## Build a prompt for Arena Agent Mode

1. Open **Arena prompt studio** and work through the ten steps. The starter brief is editable.
2. Review **Prompt Brief**. The attached evidence list contains only user-imported records; fictional demo examples are excluded. If you pin any records, the prompt includes the pinned set (up to 15); otherwise it includes up to 15 imported records.
3. Copy the brief or export it as Markdown. Open [Arena AI Agent Mode](https://arena.ai/agent) and paste it into a new chat. The app does not submit prompts to Arena automatically.
4. Generate an eval/rubric and use the same criteria to compare fresh runs. The **Best-of-N** tool only prepares prompt copies; run each copy yourself.

## Data and privacy

- Feed subscriptions, imported records, pins, and wizard answers are saved in this browser's `localStorage` under `frontier-signal-atlas-v1`.
- There is no account, remote database, analytics, AI inference, background crawl, or telemetry in this prototype.
- Avoid entering sensitive or private information. Do not use the app to collect private, login-only, or access-controlled material.
- Use **Clear imported data** on the Sources page to remove user-added records and saved feed URLs. This does not affect the original sources. Browser storage can be removed by clearing site data, so export work you need to keep.
- The app does not automatically refresh saved feeds. Use the URL intake again when you want to fetch a current snapshot.

## Limits and interpretation

- Direct RSS / Atom fetching depends on publisher CORS policy and network access; importing a local export is the fallback.
- Social-media intake is manual and limited to public content the user can access.
- Topic assignment is a small keyword heuristic, not an AI model. It can misclassify ambiguous text; verify each theme against its sources.
- Counts and coverage labels are descriptive only. They do not establish company intent, engineering ownership, hiring outcomes, product plans, or a future roadmap.
- For shared workspaces or reliable scheduled feed collection, add an authorized backend and publisher-compliant ingestion process. None is included here.

## Static hosting

The deliverable is `index.html`; no build command or generated assets are needed.

- **Cloudflare Pages:** create a Pages project connected to the repository and deploy the repository root. Leave the build command empty; set the output directory to `/` (or the root directory in the provider's UI).
- **GitHub Pages:** `.github/workflows/deploy-pages.yml` stages and deploys only `index.html` (plus `.nojekyll`) on every push to `main`; it also supports manual runs from the Actions tab. In **Settings → Pages → Build and deployment**, choose **GitHub Actions** as the source once. Merge this setup to `main` to trigger a deployment, then open the workflow's `github-pages` environment or **Settings → Pages** for the published URL (expected project URL: `https://jobsiggy.github.io/frontier-hope/`). The root `.nojekyll` file keeps Pages from running Jekyll over this static app.

## Verification checklist

- `node --check` passes on the inline JavaScript extracted from `index.html`.
- Smoke test the navigation, demo toggle, search/filter controls, prompt wizard, template actions, rubric/eval generation, quality checker, exports, and responsive layout in a browser.
- Add a representative RSS/Atom XML, JSON, and CSV file and verify that invalid URLs, malformed data, and CORS failures produce a useful error instead of claiming success.
- Confirm that generated Arena briefs exclude fictional demo rows and clearly report when no user-imported evidence is available.
