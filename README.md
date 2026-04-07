# Making changes to `tt-cric.github.io`

This site is built with **[Hugo](https://gohugo.io/)** using the **`hugo-bearblog`** theme.

---

## Quick Start

### 1) Prerequisites

Make sure you have:

- Hugo (extended version recommended)
- Git

### 2) Clone and run locally

```/dev/null/commands.sh#L1-4
git clone https://github.com/tt-cric/tt-cric.github.io.git
cd tt-cric.github.io
hugo server -D
```

Then open:

```bash
http://localhost:1313 #normally
```

`-D` includes draft posts while developing.

---

## Project Layout

```/dev/null/tree.txt#L1-20
tt-cric.github.io/
├── .github/
│   └── workflows/
│       └── hugo-deploy.yml        # GitHub Pages build/deploy pipeline
├── archetypes/
│   └── default.md                 # Default front matter template for new content
├── content/
│   ├── _index.md                  # Homepage content
│   ├── blogs/
│   │   ├── _index.md              # Blogs section index
│   │   └── starting-out.md        # Example blog post
│   └── projects/
│       └── _index.md              # Projects section index
├── layouts/
│   └── partials/
│       └── footer.html            # Site footer override/customization
├── static/                        # Static files served as-is (images, icons, etc.)
├── assets/                        # Pipeline assets (CSS/JS/images for Hugo processing)
├── data/                          # Data files used by templates
├── i18n/                          # Translation files (if needed)
├── themes/
│   └── hugo-bearblog/             # Theme (git submodule) # no need to modify this
└── hugo.toml                      # Main site configuration
```

---

## Core Configuration

Main config is in `hugo.toml`.  
Some key project-specific details:

- Base URL is set to GitHub Pages URL.
- Content types include `blogs` and `projects`.
- Permalinks are customized for cleaner URLs.
- Theme is `hugo-bearblog`.

---

## Writing Content

### Blog post front matter example

Use TOML front matter like this:

```/dev/null/blog-example.md#L1-12
+++
title = "My New Post"
date = "2026-04-07"
description = "What this post is about."
tags = ["blog", "hugo"]
draft = true
+++

Your post content goes here.
```

### Archetype defaults

The default archetype currently sets:

- `date`
- `title` (from file name)
- `draft = true`

So new posts start unpublished by default.

---

## Creating a New Blog Post

Create a new blog post:

```/dev/null/commands.sh#L1-1
hugo new content/blogs/my-new-post.md
```

Then edit the generated file and preview with:

```/dev/null/commands.sh#L1-1
hugo server -D
```

When ready to publish, set:

```/dev/null/frontmatter.toml#L1-1
draft = false
```

---

## Creating/Updating Project Pages

Project pages live under `content/projects/`.  
Create a new one similarly:

```/dev/null/commands.sh#L1-1
hugo new content/projects/my-project.md
```

Add front matter and content, then preview locally.

---

## Assets and Static Files

- Put files that should be served directly in `static/`  
  (example: `static/images/logo.png` → `/images/logo.png` on site).
- Use `assets/` for files intended for Hugo Pipes processing.

---

## Theme Notes

This project uses the `hugo-bearblog` theme via submodule:

- Avoid editing theme files directly unless necessary.
- Prefer overrides in your project’s `layouts/`, `assets/`, or `static/`.
- CI currently updates the theme submodule to the latest `master` during build.

---

## Deployment

Deployment is handled by GitHub Actions in:

- `.github/workflows/hugo-deploy.yml`

On push to `master`, it builds and deploys to GitHub Pages.

---

## Contribution Workflow

1. Create a branch from `master`.
2. Make focused changes.
3. Run locally (`hugo server -D`) and verify.
4. Commit with clear messages.
5. Open a Pull Request with:
   - What changed
   - Why it changed
   - Screenshots (if UI/content layout changed)

---

## Suggested Commit Style

Examples:

- `docs: add contributing section for blog post workflow`
- `content: add post about xyz`
- `layout: adjust footer partial links`
- `config: update permalinks for blogs`

---

## Content Guidelines

- Keep writing clear and concise.
- Use descriptive titles and summaries.
- Add relevant tags.
- Ensure links/images are valid.
- Check formatting in local preview before PR.

---

## Need Help?

If you’re unsure where to place something:

- **Blog post** → `content/blogs/`
- **Project page** → `content/projects/`
- **Site-wide config** → `hugo.toml`
- **Template override** → `layouts/`
- **Images/files** → `static/`
