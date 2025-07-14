# Jekyll Build Fix for Vercel Deployment

## Problem
The Jekyll site was failing to build on Vercel with the error:
```
sh: line 1: jekyll: command not found
Error: Command "jekyll build" exited with 127
```

## Root Cause
The site was configured for GitHub Pages but lacked proper configuration for Vercel deployment:
- No `Gemfile` to specify Ruby dependencies
- No `vercel.json` for build configuration
- Minimal `_config.yml` configuration
- No Ruby version specification

## Solution
Created the following files to fix the build:

### 1. `Gemfile`
- Specified Jekyll and theme dependencies
- Added common Jekyll plugins (feed, sitemap, seo-tag)

### 2. `vercel.json`
- Configured Vercel to use `@vercel/static-build`
- Set build command: `bundle install && bundle exec jekyll build`
- Set output directory to `_site`
- Specified install command for dependencies

### 3. `package.json`
- Added build script for Vercel compatibility
- Provides fallback build configuration

### 4. Updated `_config.yml`
- Added proper site settings
- Configured Jekyll plugins
- Added file exclusions for cleaner builds

### 5. `.ruby-version`
- Specified Ruby 3.0.0 for consistent builds

## Next Steps
1. Commit and push these files to the repository
2. Redeploy on Vercel - the build should now succeed
3. The site will be built using Jekyll and served from the `_site` directory

## Alternative Solutions
If you prefer to stay with GitHub Pages:
- Keep using the original minimal setup
- Deploy directly from the `gh-pages` branch on GitHub
- Use the GitHub Pages URL instead of Vercel