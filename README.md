# Ivory — Minimal Static Site Builder

Ivory is a lightweight static site builder written in Python. It converts Markdown content with front matter into HTML using a simple layout system, copies static assets, generates a sitemap, and optionally serves the output locally for preview.



## Overview

Ivory provides:

* Markdown → HTML conversion
* YAML front matter parsing
* Layout-driven page rendering
* Static asset copying
* Post listing generation
* Sitemap generation
* Tailwind CSS compilation
* Local preview server

The build output is written to the `public/` directory.



## Requirements

* Python 3.x
* Node.js (for Tailwind CSS)

### Python Dependencies

Install required packages:

```bash
pip install python-frontmatter markdown
```

### Node Dependency

```bash
npm install -D tailwindcss
```



## Project Structure

```
project/
│
├── ivory.py
├── siteconfig.ivory.md
│
├── markdown/
│   ├── *.md
│   └── post/
│       ├── *.md
│       └── index.md
│
├── layouts/
│   ├── base.html
│   ├── head.html
│   ├── header.html
│   ├── footer.html
│   ├── root_single.html
│   ├── post_single.html
│   └── list.html
│
├── static/
│   └── assets (images, css, js, etc.)
│
├── src/
│   └── input.css
│
└── public/
```



## Configuration

Ivory uses a Markdown configuration file:

**`siteconfig.ivory.md`**

```yaml

site: My Site
baseURL: /
title: My Site
author: Author Name

```

Generate it via:

```bash
python3 ivory.py --create
```



## Commands

### Create Project Configuration

```bash
python3 ivory.py --create
```

Prompts for:

* Site name
* Base URL
* Author



### Build Site

```bash
python3 ivory.py --build
```

Actions:

* Reads Markdown files
* Parses front matter
* Renders pages using layouts
* Copies static assets
* Generates sitemap
* Compiles Tailwind CSS



### Serve Locally

```bash
python3 ivory.py --serve
```

* Starts a local HTTP server
* Uses a random port if unspecified

Specify port:

```bash
python3 ivory.py --serve -p 8000
```

Valid range: **1000–9999**



### Build + Serve

```bash
python3 ivory.py --finalise
```

Builds the site and immediately launches the preview server.



### Create New Page

```bash
python3 ivory.py --newPage <name>
```

Creates:

```
markdown/<name>.md
```

Prompts for page title.



### Help

```bash
python3 ivory.py --help
```

Displays command usage.



## Content Authoring

Markdown files require front matter:

```yaml

title: Page Title
date: Month Day,Year

```

Example:

```markdown

title: First Post
date: February 22,2026


# Hello World
Content goes here.
```

Posts must be placed in:

```
markdown/post/
```



## Layout System

Ivory renders pages using HTML templates:

* `base.html` — main wrapper
* `head.html`, `header.html`, `footer.html`
* `root_single.html` — standard pages
* `post_single.html` — blog posts
* `list.html` — post index

Templates use Python `.format()` placeholders:

```
{Content}
{Title}
{Site}
{date}
{author}
{Summary}
{wordCount}
{readingTime}
{stylesPermalink}
```



## Exclusive Pages

Files in `layouts/` prefixed with `_` are copied directly:

```
_about.html → public/about.html
```

Use for custom standalone pages.



## Sitemap

Generated automatically:

```
public/sitemap.xml
```

Based on `sitemap_template`.



## Styling

Tailwind CSS is compiled during build:

```bash
npx tailwindcss -i ./src/input.css -o ./public/stylesheet.css
```

Ensure:

* Tailwind installed
* `src/input.css` exists



## Output

All generated files are placed in:

```
public/
```

Structure:

```
public/
├── index.html
├── *.html
├── post/
│   └── *.html
└── sitemap.xml
```



## Notes

* Build clears previously generated HTML files
* Reading time is estimated from word count
* Posts are ordered by creation time
* Tailwind compilation runs on every build



## License

MIT.


