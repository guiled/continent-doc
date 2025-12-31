# GitHub Pages Setup

This repository is configured to work with GitHub Pages using Jekyll.

## Quick Start

1. **Push to GitHub**: Push this repository to GitHub
2. **Enable GitHub Pages**: 
   - Go to your repository Settings
   - Navigate to Pages section
   - Select source branch (usually `main` or `gh-pages`)
   - Save

GitHub Pages will automatically build and deploy your site using Jekyll.

## Local Development

To test the site locally before pushing:

1. **Install Ruby and Bundler** (if not already installed):
   ```bash
   # macOS (using Homebrew)
   brew install ruby
   
   # Or use rbenv/rvm
   ```

2. **Install dependencies**:
   ```bash
   bundle install
   ```

3. **Run Jekyll locally**:
   ```bash
   bundle exec jekyll serve
   ```

4. **View site**: Open http://localhost:4000 in your browser

## File Structure

- `_config.yml` - Jekyll configuration
- `_layouts/` - HTML layouts for pages
- `assets/css/` - Stylesheets
- `index.md` - Homepage (converted from index.html)
- `*.md` - All markdown files with Jekyll front matter
- `Gemfile` - Ruby dependencies for local development

## How It Works

- Jekyll automatically converts all `.md` files to `.html`
- Files with front matter (YAML header) are processed as pages
- The `default` layout wraps all pages with navigation and footer
- Links in markdown use Jekyll's `relative_url` filter for proper paths

## Customization

- **Navigation**: Edit `navigation` section in `_config.yml`
- **Styling**: Modify `assets/css/style.css`
- **Layout**: Edit `_layouts/default.html`
- **Theme**: Change `theme` in `_config.yml` (currently using `minima`)

## Notes

- GitHub Pages uses a specific set of Jekyll plugins (see `Gemfile`)
- Some Jekyll plugins may not work on GitHub Pages
- The site will rebuild automatically on each push to the selected branch

