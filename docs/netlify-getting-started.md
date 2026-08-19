---
id: netlify-getting-started
title: Getting Started with Netlify
displayed_sidebar: null
hide_table_of_contents: false
---

# Getting Started with Netlify: Deploy a Static Site from GitHub

## Overview

Netlify lets you deploy and host static sites directly from a GitHub repository. This guide walks you through connecting a GitHub repo to Netlify and deploying a site with in a live URL that updates automatically every time you push changes to your repo. This guide uses Docusaurus as the statis site generator, but information pertaining to Hugo and Jekyll is noted.

## Prerequisites

Before beginning the steps outlined in this guide, you need the following:

- A GitHub account
- A static site project already committed to a GitHub repository
- A static site generator configured in your project (such as Docusaurus, Hugo, or Jekyll) with a defined build command and output directory
- Basic familiarity with Git (committing and pushing changes)
- Node.js installed if your static site generator requires it (for example, Docusaurus requires Node.js v18 or higher)

## Step 1: Create a Netlify Account

1. Go to [netlify.com](https://www.netlify.com) and click the  **Sign up** button.
2. Click the **Sign up with GitHub** button to authenticate using your existing GitHub account. This simplifies the connection between Netlify and your repositories in the next step.
3. When prompted, authorize the Netlify GitHub App.

Once successfully authenticated, you will be directed to the Netlify dashboard, where you can manage your sites and deployments.

## Step 2: Connect Your GitHub Repository

1. On the Netlify dashboard, click **Add new project**.
2. On the project details page, click the **GitHub** button.
3. Authorize Netlify to access your GitHub repositories when prompted. For security, grant access only to the specific repository you want to deploy rather than all repositories.
4. Search for and select your repository from the list.

## Step 3: Configure Build Settings

Netlify will attempt to auto-detect your build settings based on your static site generator. Review the following fields and confirm or update them as needed:

- **Branch to deploy:** The branch Netlify will monitor for changes. This is typically `main`.
- **Build command:** The command Netlify runs to build your site. For Docusaurus, this is `npm run build`. For Hugo, this is `hugo`. For Jekyll, this is `jekyll build`.
- **Publish directory:** The folder containing your built site files that Netlify will serve. For Docusaurus, this is `build`. For Hugo and Jekyll, this is `public`.

If Netlify detects your static site generator correctly, these fields may already be populated. Verify them before proceeding.

## Troubleshooting

### Broken links error

If your build fails with a message like `Error: Docusaurus found broken links`, your site contains links pointing to pages that don't exist yet. You have two options:

- **Fix the broken links** by creating the missing pages or updating the links to point to existing content.
- In the `docusaurus.config.js` file, **temporarily set `onBrokenLinks` to `warn`**  to allow the build to complete while you build out your content. After the broken links are resolved, change the `onBrokenLinks` setting back to `throw`.

### Build command not recognized

If Netlify can't find or run your build command, verify that:

- The build command matches your static site generator exactly (commands are case-sensitive)
- Your repository includes the necessary configuration files for your static site generator
- Any required dependencies are listed in your `package.json` if you're using a Node.js-based generator

### Site deploys but shows default content

If the live site shows Netlify's default placeholder page rather than your site content, your publish directory may be incorrect. Verify the publish directory in your Netlify build settings matches the actual output folder your static site generator produces.

## Next Steps

Now that your site is live, consider the following:

- **Customize your site URL:** By default, Netlify assigns a randomly generated URL. To specify a custom URL, open the project and click **Project configuration**. In the General Project Settings page, locate the **Project details** section, and clik the **Change project name** button. The Netlify modal will display a preview of the custom URL.
- **Add a custom domain:** If you own a domain name, you can connect it to your Netlify site. To add your domain, open the project and click the **Domain management** link in the sidebar.
- **Set up branch deploys:** Configure Netlify to create preview deployments for pull requests and feature branches, so changes can be reviewed before merging to the main branch.
- **Explore Netlify's CI/CD pipeline:** In the sidebar, click the **Builds** link to review the build log for each deployment and gain insight about how Netlify builds and publishes your site automatically on every push.