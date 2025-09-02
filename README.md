# Deploy Dhall Documentation to GitHub Pages

A reusable GitHub Actions workflow for automatically generating and deploying Dhall documentation to GitHub Pages.

## Overview

This repository contains a GitHub Actions workflow that:
- Generates documentation from Dhall source files
- Deploys the generated documentation to GitHub Pages
- Provides a reliable, automated documentation pipeline for Dhall projects

## Usage

1. Copy the `.github/workflows/main.yaml` file to your Dhall project repository
2. Ensure your Dhall source files are in a `src` directory (or modify the workflow to point to your source directory)
3. Enable GitHub Pages in your repository settings
4. Run the workflow manually via the "Actions" tab or trigger it programmatically

## Workflow Features

- **Manual Trigger**: Uses `workflow_dispatch` for on-demand documentation generation
- **Concurrency Control**: Prevents overlapping deployments
- **Proper Permissions**: Configured for secure GitHub Pages deployment
- **Dhall Documentation**: Uses the specialized `nikita-volkov/dhall-docs.github-action` for accurate Dhall documentation generation

## Requirements

- Dhall source files in your repository
- GitHub Pages enabled
- Appropriate repository permissions for GitHub Actions

## Customization

The workflow can be customized by:
- Changing the `input` parameter to point to a different source directory
- Modifying the trigger conditions (e.g., adding `push` triggers)
- Updating action versions as they become available

## About Dhall

Dhall is a programmable configuration language that is statically typed and strongly normalizing. Learn more at [dhall-lang.org](https://dhall-lang.org/).