# Deploy Dhall Documentation to GitHub Pages

A GitHub Actions workflow template for automatically generating and deploying Dhall documentation to GitHub Pages.

## Overview

This repository provides a reusable GitHub Actions workflow that:

1. **Generates** Dhall documentation from your source files using the [`dhall-docs`](https://github.com/nikita-volkov/dhall-docs.github-action) action
2. **Deploys** the generated documentation to GitHub Pages automatically
3. **Manages** concurrent deployments to prevent conflicts

## Features

- 🚀 **Automated deployment** - Trigger manually or integrate with your CI/CD pipeline
- 📚 **Documentation generation** - Uses the official Dhall documentation generator
- 🔒 **Secure** - Uses GitHub's built-in OIDC tokens for authentication
- ⚡ **Concurrent-safe** - Prevents overlapping deployments
- 🎯 **Simple setup** - Minimal configuration required

## Prerequisites

Before using this workflow, ensure your repository has:

1. **Dhall source files** in a `src` directory (or specify a custom path)
2. **GitHub Pages enabled** in your repository settings
3. **Appropriate permissions** for the workflow to deploy to Pages

## Quick Start

### 1. Enable GitHub Pages

1. Go to your repository **Settings** → **Pages**
2. Under **Source**, select **GitHub Actions**

### 2. Copy the Workflow

Create `.github/workflows/deploy-dhall-docs.yml` in your repository:

```yaml
name: Deploy Dhall Documentation to GitHub Pages

on:
  # Trigger on pushes to main branch
  push:
    branches: [ main ]
  # Allow manual triggering
  workflow_dispatch:

# Prevent overlapping publishes on rapid pushes
concurrency:
  group: deploy-dhall-docs-to-github-pages
  cancel-in-progress: true

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build-docs:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deploy.outputs.page_url }}
    steps:
      - uses: actions/checkout@v4

      - name: Generate docs
        id: generate-docs
        uses: nikita-volkov/dhall-docs.github-action@v0.3
        with:
          input: src

      - name: Upload artifact for Pages
        uses: actions/upload-pages-artifact@v4
        with:
          path: ${{ steps.generate-docs.outputs.path }}

      - name: Deploy to GitHub Pages
        id: deploy
        uses: actions/deploy-pages@v4
```

### 3. Trigger the Workflow

- **Automatically**: Push changes to your main branch
- **Manually**: Go to **Actions** → **Deploy Dhall Documentation to GitHub Pages** → **Run workflow**

## Configuration Options

### Custom Source Directory

If your Dhall files are not in a `src` directory, modify the `input` parameter:

```yaml
- name: Generate docs
  uses: nikita-volkov/dhall-docs.github-action@v0.3
  with:
    input: path/to/your/dhall/files
```

### Different Trigger Events

Customize when the workflow runs by modifying the `on` section:

```yaml
on:
  # On pushes to specific branches
  push:
    branches: [ main, develop ]
    paths: [ 'src/**' ]  # Only when Dhall files change
  
  # On pull requests
  pull_request:
    branches: [ main ]
  
  # On a schedule (daily at midnight UTC)
  schedule:
    - cron: '0 0 * * *'
  
  # Manual trigger
  workflow_dispatch:
```

## Repository Structure

For this workflow to work effectively, organize your repository like this:

```
your-repository/
├── .github/
│   └── workflows/
│       └── deploy-dhall-docs.yml
├── src/                    # Your Dhall source files
│   ├── Config.dhall
│   ├── Types.dhall
│   └── ...
├── README.md
└── ...
```

## Permissions

The workflow requires the following permissions:

- `contents: read` - To checkout the repository
- `pages: write` - To deploy to GitHub Pages
- `id-token: write` - For secure authentication with GitHub Pages

These are automatically granted when you use the provided workflow configuration.

## Troubleshooting

### Common Issues

**📄 Pages not updating**: Ensure GitHub Pages is configured to use "GitHub Actions" as the source in your repository settings.

**🔒 Permission denied**: Verify that the `pages: write` and `id-token: write` permissions are set in your workflow.

**📁 No Dhall files found**: Check that your Dhall files are in the correct directory (default: `src`) or update the `input` parameter.

**🚫 Deployment failed**: Check the Actions logs for detailed error messages. Common causes include malformed Dhall files or missing dependencies.

### Getting Help

- Check the [dhall-docs action documentation](https://github.com/nikita-volkov/dhall-docs.github-action)
- Review the [GitHub Pages documentation](https://docs.github.com/en/pages)
- Open an issue in this repository for workflow-specific problems

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests to improve this workflow template.

## License

This workflow template is provided as-is for use in your projects. See individual action licenses for their respective terms.