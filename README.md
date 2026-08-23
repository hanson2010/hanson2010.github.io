# Hanson's weblog

This is the source of [Hanson's weblog](https://blog.pythoner.work), built with [Hugo](https://gohugo.io/) and deployed on [Cloudflare Pages](https://pages.cloudflare.com/).

## Tech stack

- **Static site generator:** [Hugo (extended)](https://gohugo.io/), currently `0.148.2`
- **Theme:** [PaperMod](https://github.com/adityatelange/hugo-PaperMod), vendored as a git submodule at `themes/papermod`
- **Hosting / CI:** Cloudflare Pages, building directly from this repo on every push to `main` (no GitHub Actions workflow is used)
- **Content:** Bilingual (English / Chinese) Markdown posts

## Project structure

```
config/_default/     # Split Hugo config: hugo.yml, params.yml, languages.en.yml, languages.zh.yml
content/posts/       # Blog posts, organized as content/posts/<year>/<slug>/index.md
archetypes/          # `hugo new` post template
static/              # Files served as-is (favicon, CNAME, images)
themes/papermod/     # PaperMod theme (git submodule)
```

Posts are Hugo [page bundles](https://gohugo.io/content-management/page-bundles/) — each lives in its own folder (`content/posts/<year>/<slug>/index.md`) alongside any images it references.

## Local development

Clone the repo with submodules (needed to pull in the PaperMod theme):

```sh
git clone --recurse-submodules https://github.com/hanson2010/hanson2010.github.io.git
```

If you already cloned without `--recurse-submodules`:

```sh
git submodule update --init --recursive
```

Requires the **extended** edition of Hugo (`0.148.2`, matching production — see [Deployment](#deployment)).

Run the dev server with drafts and future-dated posts visible:

```sh
hugo server -D -F
```

Build the site to `public/` (matches the production build):

```sh
hugo
```

## Writing a new post

```sh
hugo new posts/<year>/<slug>/index.md
```

This uses `archetypes/default.md`, which sets `date` and `draft: true`. Add `title`, `categories`, and `tags` manually — see existing posts under `content/posts/` for conventions. Set `draft: false` when ready to publish.

## Deployment

The site is hosted on **Cloudflare Pages**, connected directly to this GitHub repository. Cloudflare builds and deploys automatically on every push to `main` (and generates preview deployments for other branches/PRs). Dashboard build settings:

| Setting | Value |
|---|---|
| Build command | `hugo` |
| Build output directory | `public` |
| Environment variable | `HUGO_VERSION=0.148.2` |

There is no build configuration checked into this repo (an earlier GitHub Actions + GitHub Pages workflow was removed when the project moved to Cloudflare Pages) — the settings above live only in the Cloudflare Pages dashboard.

## Updating the theme

The theme is a git submodule. To pull in updates:

```sh
git submodule update --remote themes/papermod
git add themes/papermod
git commit -m "Update papermod theme"
```
