# Deploy Dhall Documentation to GitHub Pages

A GitHub Actions workflow template for automatically generating and deploying Dhall documentation to GitHub Pages.

## Overview

This repository provides a reusable GitHub Actions workflow that:

- **Generates** Dhall documentation from your source files using the [`dhall-docs`](https://github.com/nikita-volkov/dhall-docs.github-action) action
- **Deploys** the generated documentation to GitHub Pages automatically

## Quick Start

### 1. Enable GitHub Pages

1. Go to your repository **Settings** → **Pages**
2. Under **Source**, select **GitHub Actions**

### 2. Copy the Workflow

Create `.github/workflows/deploy-dhall-docs.yml` in your repository:

```yaml
name: Deploy Dhall Documentation to GitHub Pages

on:
  # Trigger on pushes to main or master branch
  push:
    branches: [ main, master ]
  # Allow manual triggering
  workflow_dispatch:

jobs:
  build-docs:
    uses: nikita-volkov/deploy-dhall-docs-to-github-pages.github-actions-workflow/.github/workflows/main.yaml@v1
    with:
      input: src # Optional: Path to your Dhall source directory (default: .)
      package-name: typeclasses # Optional: Package name for documentation
    secrets: inherit
```

### 3. Trigger the Workflow

- **Automatically**: Push changes to your main branch
- **Manually**: Go to **Actions** → **Deploy Dhall Documentation to GitHub Pages** → **Run workflow**

## Configuration Options

The workflow accepts the following inputs that you can customize:

### `input`

**Description**: Path to the directory containing your Dhall source files  
**Required**: No  
**Default**: `.`

**Example**:
```yaml
jobs:
  build-docs:
    uses: nikita-volkov/deploy-dhall-docs-to-github-pages.github-actions-workflow/.github/workflows/main.yaml@v1
    with:
      input: dhall-src  # If your Dhall files are in 'dhall-src'
```

### `package-name`

**Description**: Name of your Dhall package to display in the generated documentation  
**Required**: No  
**Default**: None

**Example**:
```yaml
jobs:
  build-docs:
    uses: nikita-volkov/deploy-dhall-docs-to-github-pages.github-actions-workflow/.github/workflows/main.yaml@v1
    with:
      package-name: my-awesome-dhall-library
```

## Troubleshooting

### Common Issues

**📄 Pages not updating**: Ensure GitHub Pages is configured to use "GitHub Actions" as the source in your repository settings.

**🔒 Permission denied**: Verify that the `pages: write` and `id-token: write` permissions are set in your workflow.

**📁 No Dhall files found**: Check that your Dhall files are in the correct directory (default: `src`) or update the `input` parameter in your workflow configuration.
