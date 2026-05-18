# bamcgill.github.io — Jekyll Blog

Migrated from Blogspot (barrymcgillin.blogspot.com) → Jekyll + GitHub Pages.

## What's Here

- `_posts/` — 91 published blog posts (2007–2019), converted to Markdown
- `_drafts/` — 14 draft posts (including your SQLcl MCP server post from July 2025)
- `_config.yml` — Site configuration (Minimal Mistakes theme, dark skin)
- `_pages/` — About, Tags, Categories pages
- `_data/navigation.yml` — Top nav bar
- `assets/images/avatar.jpg` — Your profile photo
- `assets/images/posts/` — Blog images from the Blogger export

## How to Deploy

### Option 1: Push directly to GitHub (quickest)

```bash
# Clone your existing repo
git clone git@github.com:bamcgill/bamcgill.github.io.git
cd bamcgill.github.io

# Remove the old placeholder content
git rm -rf .
git clean -fd

# Copy the Jekyll site contents into the repo root
cp -r /path/to/this/jekyll_site/* .
cp -r /path/to/this/jekyll_site/.* . 2>/dev/null

# Commit and push
git add -A
git commit -m "Migrate blog from Blogspot to Jekyll + Minimal Mistakes"
git push origin main
```

GitHub Pages will build the site automatically. Give it a couple of minutes,
then visit https://bamcgill.github.io

### Option 2: Test locally first

```bash
# Install Ruby and Bundler if needed
gem install bundler

# Install dependencies
bundle install

# Run locally
bundle exec jekyll serve

# Visit http://localhost:4000
```

## Custom Domain

To use a custom domain (e.g., blog.barrymcgillin.com):

1. Create a `CNAME` file in the repo root containing just the domain name
2. Add a CNAME DNS record pointing your domain to `bamcgill.github.io`
3. Enable HTTPS in GitHub repo Settings → Pages

## Publishing Drafts

To publish a draft, move it from `_drafts/` to `_posts/`. The filename
already has the date prefix, so it's ready to go.

## Images

Post images currently reference Blogger-hosted URLs, which will continue
working. The `assets/images/posts/` folder contains local copies if you
want to update the image references later for full self-hosting.

## Theme Customisation

The site uses the Minimal Mistakes theme (dark skin). To change the skin,
edit `minimal_mistakes_skin` in `_config.yml`. Options: air, aqua,
contrast, dark, default, dirt, mint, neon, plum, sunrise.

## Notes

- The Coderdojoomagh blog was also in the export but not included here.
  Let me know if you want that migrated too.
- Some older posts have HTML artefacts from Blogspot's editor — these
  are cosmetic and can be cleaned up over time.
- Update the LinkedIn URL in `_config.yml` if yours differs.
