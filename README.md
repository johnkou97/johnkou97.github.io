# koutalios.space

Personal website of Ioannis Koutalios — data scientist and astrophysicist.
Live at **[koutalios.space](https://koutalios.space)**.

Built with [Jekyll](https://jekyllrb.com/) on the
[al-folio](https://github.com/alshedivat/al-folio) theme
(MIT, © 2022 Maruan Al-Shedivat). Site content © 2026 Ioannis Koutalios.

## Structure

| Path             | Contents                                                      |
| ---------------- | ------------------------------------------------------------- |
| `_pages/`        | About, Projects, Publications, CV, 404                        |
| `_projects/`     | Project pages, grouped as `research` / `courses` / `personal` |
| `_bibliography/` | `papers.bib` (own publications), `external.bib` (works cited) |
| `assets/json/`   | `resume.json` — source of the CV page                         |
| `_includes/`     | Liquid partials · `_layouts/` page layouts · `_sass/` styles  |

## Running locally

No Ruby needed — use Docker:

```bash
docker compose up --build
```

Then open <http://localhost:8080>. The working directory is mounted, so edits
reload live. `--build` builds from the local `Dockerfile` rather than pulling
the upstream prebuilt image, which keeps the gems in step with `Gemfile`.

With a local Ruby toolchain instead:

```bash
bundle install
bundle exec jekyll serve
```

## Before pushing

CI runs Prettier on every push and fails the build on formatting drift:

```bash
npx prettier . --check     # add --write to fix
```

## Deployment

Pushing to `master` triggers `.github/workflows/deploy.yml`, which builds the
site, purges unused CSS, and publishes the result to the `gh-pages` branch —
which is what GitHub Pages serves. `gh-pages` is generated output; never edit
it by hand. A second workflow then link-checks the built site.
