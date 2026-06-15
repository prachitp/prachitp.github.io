# Website Template - Setup Guide

This is the Jekyll source of kulbir-singh-ahluwalia.com, stripped of personal
images, PDFs, and course pages so you can use it as a template. It is a
single-page academic/professional portfolio with sections for news,
publications, projects, and links, all driven by YAML data files.

Strategy reminder: get a basic site live with real CONTENT first (bio,
education, experience, links); photos and polish come later. A placeholder
profile image is fine for launch. For layout inspiration, Kulbir also
suggested https://keunhong.com/ and https://vsimkus.github.io/academic-jekyll/
- this template is the ready-to-deploy third option.

## What was removed (you supply your own)

- `images/` - empty; add your profile photo and any figures here
- `files/` - empty; add your resume/CV PDFs and paper PDFs here
- `CNAME.example` - inert reference copy of the custom-domain file. Do NOT
  rename it to `CNAME` until the domain step: an active CNAME makes
  prachitp.github.io redirect to the domain before DNS works. The GitHub
  Pages UI creates the real `CNAME` for you in Part C of the launch guide.
- `cs498gc/` course pages - removed (course-specific content)
- The previous owner's AI-assistant config (`AGENTS.md`/`CLAUDE.md` files,
  `.cursor/` rules, a Claude GitHub workflow, `update_nav.py`) - removed

The HTML still references some image/file paths that are now empty. Replace
them with your own assets as you edit; the site builds fine regardless.

## Where the content lives (edit these, mostly not the HTML)

| File | What it controls |
|---|---|
| `_config.yml` | Your name, title, position, email, bio paragraph, social links |
| `_data/navigation.yml` | Top navigation bar entries |
| `_data/news.yml` | News/updates list |
| `_data/publications.yml` | Publication entries (title, authors, venue, links) |
| `_data/projects.yml` | Project cards |
| `_data/authors.yml` | Co-author names and homepage links |
| `_data/hobbies.yml`, `_data/misc.yaml`, `_data/quote.txt` | Optional extras |
| `index.html` | Page structure - touch only to add/remove whole sections |
| `cv.html` | CV page wrapper |
| `css/`, `_sass/` | Styling |

Search-and-replace pass before publishing: grep the tree (case-insensitive,
so it also catches the old domain kulbir-singh-ahluwalia.com and lowercase
mentions) and replace every hit with your own details:

```bash
grep -rniE "kulbir|ksa5" --include="*.yml" --include="*.yaml" --include="*.html" --include="*.json" .
```

Repeat until that command returns nothing.

## Run locally

Requires Ruby 3.x and Bundler. On macOS, do NOT use the system Ruby
(`gem install` against it fails without sudo); use Homebrew's:

```bash
brew install ruby
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc          # Homebrew ruby is keg-only; it must be put on PATH
gem install bundler
bundle install
bundle exec jekyll serve
# open http://127.0.0.1:4000
```

On Ubuntu: `sudo apt install ruby-full build-essential`, then the same
`gem install bundler` onward.

## Deploy free on GitHub Pages

1. Create a GitHub repository named exactly `prachitp.github.io`.
2. Copy this template's contents in, commit, push to the `main` branch.
3. Repo Settings -> Pages -> Source: deploy from `main` branch root.
4. Your site is live at `https://prachitp.github.io` within minutes.

## Custom domain: prachit-puranik.com

Your domain is `prachit-puranik.com`, registered on Squarespace, and `url:`
in `_config.yml` is already set to it. Connect it AFTER the site works at
prachitp.github.io: follow Part C of `START-HERE-WEBSITE-GUIDE.md` (kit
root), with full DNS details and `dig` verification commands in
`PRACHIT-DOMAIN-SETUP.md`.

## Notes

- `.github/workflows/cache_control.yml` adds HTTP cache headers on every push
  to `main`. Harmless to keep; delete it if you want the bare minimum.
- `environment.yml` and `spec/` are conveniences from the original repo; safe
  to delete if unused.
