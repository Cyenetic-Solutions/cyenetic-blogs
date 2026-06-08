# Cloudflare Pages Deployment Guide

This guide explains how to deploy the Cyenetic blog to Cloudflare Pages.

## Prerequisites

1. A Cloudflare account
2. Access to your GitHub repository

## Setup Steps

### 1. Create a Cloudflare Pages Project

1. Log in to [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. Go to **Workers & Pages** → **Pages**
3. Click **Create a project** → **Connect to Git**
4. Authorize GitHub and select the `cyenetic-blog` repository
5. Choose **main** as the production branch
6. For build settings:
   - **Framework preset**: None
   - **Build command**: `bundle install && bundle exec jekyll build`
   - **Build output directory**: `_site`
   - **Environment variables**: (optional) Add any Jekyll environment variables
7. Click **Save and Deploy**

### 2. Configure Custom Domain (Optional)

1. In Cloudflare Pages, go to your project settings
2. Click **Custom domains**
3. Add your domain (e.g., `blogs.cyenetic.com`)
4. Update your domain's nameservers to point to Cloudflare (if not already using Cloudflare DNS)

## Manual Deployment

To deploy your site:

1. **Push your changes** to the `main` branch:
   ```bash
   git add .
   git commit -m "Your commit message"
   git push origin main
   ```

2. **Trigger deployment from Cloudflare**:
   - Go to your project in Cloudflare Pages
   - Click **Deployments**
   - Click **Trigger deployment** → **Deploy latest commit**
   - Wait for the build to complete (usually 1-2 minutes)

3. **Your site is live** at `https://cyenetic-blog.pages.dev` (or your custom domain)

## Local Testing

Test your site locally before pushing:

```bash
bundle install
bundle exec jekyll serve
```

Then visit `http://localhost:4000`

## Build Configuration

The build process is configured in Cloudflare Pages:
- Uses Ruby 3.2 with bundler (Cloudflare's default)
- Builds Jekyll to `_site` directory
- Serves from Cloudflare's global network

## Troubleshooting

### Build Fails
- Check the Cloudflare Pages build logs
- Ensure `Gemfile.lock` is committed to the repository
- Verify all required gems are in the Gemfile

### Site Not Updating
- Make sure commits are pushed to the `main` branch
- Verify you triggered the deployment in Cloudflare Pages
- Clear your browser cache if changes don't appear

## Additional Resources

- [Cloudflare Pages Documentation](https://developers.cloudflare.com/pages/)
- [Jekyll Documentation](https://jekyllrb.com/docs/)
