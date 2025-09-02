# Copilot Instructions

## Repository Overview

This repository contains a reusable GitHub Actions workflow for automatically deploying Dhall documentation to GitHub Pages. It's designed to be used as a template or reference for projects that need to generate and publish Dhall documentation.

## Repository Structure

- `.github/workflows/main.yaml`: The main GitHub Actions workflow that handles documentation generation and deployment
- `README.md`: Basic repository documentation
- `.github/copilot-instructions.md`: This file - provides context for GitHub Copilot

## Workflow Functionality

The GitHub Actions workflow (`main.yaml`) performs the following operations:

1. **Trigger**: Runs on `workflow_dispatch` (manual trigger)
2. **Documentation Generation**: Uses the `nikita-volkov/dhall-docs.github-action@v0.3` action to generate documentation from a `src` directory
3. **Deployment**: Uploads the generated documentation to GitHub Pages using the standard Pages deployment actions

## Key Components

### Workflow Configuration
- **Concurrency**: Prevents overlapping deployments with `cancel-in-progress: true`
- **Permissions**: Configured for GitHub Pages deployment (contents: read, pages: write, id-token: write)
- **Environment**: Uses the `github-pages` environment

### Dependencies
- `actions/checkout@v4`: For repository checkout
- `nikita-volkov/dhall-docs.github-action@v0.3`: Custom action for Dhall documentation generation
- `actions/upload-pages-artifact@v4`: For uploading documentation artifacts
- `actions/deploy-pages@v4`: For GitHub Pages deployment

## Dhall Context

Dhall is a programmable configuration language that is statically typed and strongly normalizing. This workflow is specifically designed for projects using Dhall that need to:
- Generate API documentation from Dhall source files
- Host that documentation on GitHub Pages
- Automate the deployment process

## Modification Guidelines

When working with this workflow:

1. **Source Directory**: The workflow expects Dhall source files in a `src` directory. If your project uses a different structure, update the `input` parameter in the workflow.

2. **Action Version**: The workflow uses `nikita-volkov/dhall-docs.github-action@v0.3`. Check for newer versions when updating.

3. **Permissions**: Ensure your repository has GitHub Pages enabled and the workflow has appropriate permissions.

4. **Environment**: The workflow uses the `github-pages` environment, which may require approval for deployments depending on your repository settings.

## Usage

This workflow is intended to be:
- Copied to other repositories that need Dhall documentation deployment
- Used as a reference for similar documentation workflows
- Customized for specific project needs

## Testing

Since this is a GitHub Actions workflow repository:
- Test changes by running the workflow in a test repository
- Verify that documentation generates correctly
- Ensure GitHub Pages deployment works as expected
- Check that the workflow handles different Dhall project structures

## Common Issues

- Ensure the `src` directory exists and contains valid Dhall files
- Verify GitHub Pages is enabled in repository settings
- Check that the repository has the necessary permissions for Pages deployment
- Confirm the `nikita-volkov/dhall-docs.github-action` is accessible and functional