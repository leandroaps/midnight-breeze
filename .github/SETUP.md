# GitHub Action Setup for VSCode Extension Publishing

This repository includes a GitHub Action that automatically builds and publishes your VSCode theme to the Visual Studio Code Marketplace.

## Prerequisites

Before the GitHub Action can publish your extension, you need to set up the following:

### 1. Visual Studio Code Marketplace Publisher Account

1. Go to [Visual Studio Marketplace Publisher Management](https://marketplace.visualstudio.com/manage)
2. Sign in with your Microsoft account
3. Create a publisher account if you don't have one
4. Note your publisher name (should match the `publisher` field in `package.json`)

### 2. Personal Access Token (PAT)

1. Go to [Azure DevOps](https://dev.azure.com)
2. Sign in with the same Microsoft account
3. Click on your profile picture → Security
4. Click "Personal access tokens"
5. Click "New Token"
6. Configure the token:
   - **Name**: `VSCode Extension Publishing`
   - **Organization**: Select your organization
   - **Expiration**: Choose appropriate duration (recommend 1 year)
   - **Scopes**: Select "Custom defined" and check:
     - **Marketplace** → **Manage**
7. Click "Create" and copy the token (you won't see it again!)

### 3. GitHub Repository Secrets

1. Go to your GitHub repository
2. Click **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**
4. Add the following secret:
   - **Name**: `VSCE_PAT`
   - **Value**: The Personal Access Token you created above

## How to Use

### Automatic Publishing (Recommended)

1. Update the version in `package.json`
2. Commit your changes
3. Create and push a git tag:

   ```bash
   git tag v1.0.3
   git push origin v1.0.3
   ```

4. The GitHub Action will automatically:
   - Build the extension
   - Publish to VS Code Marketplace
   - Create a GitHub release
   - Upload the VSIX file as a release asset

### Manual Publishing

1. Go to your repository on GitHub
2. Click **Actions** → **Publish VSCode Extension**
3. Click **Run workflow**
4. Enter the version number (e.g., `1.0.3`)
5. Click **Run workflow**

## Workflow Features

- ✅ Automatic building and packaging
- ✅ Publishing to VS Code Marketplace
- ✅ Creating GitHub releases
- ✅ Uploading VSIX files as artifacts
- ✅ Support for both tag-based and manual triggers
- ✅ Version management

## Troubleshooting

### Common Issues

1. **"Publisher not found"**: Make sure the `publisher` field in `package.json` matches your marketplace publisher name
2. **"Invalid PAT"**: Regenerate your Personal Access Token and update the GitHub secret
3. **"Version already exists"**: Make sure to increment the version number in `package.json`

### Checking Logs

1. Go to **Actions** tab in your GitHub repository
2. Click on the failed workflow run
3. Expand the failed step to see detailed error messages

## Version Management

The workflow supports two versioning approaches:

1. **Git Tags**: Version is taken from the git tag (e.g., `v1.0.3`)
2. **Manual Input**: Version is specified when manually triggering the workflow

Make sure the version follows semantic versioning (e.g., `1.0.3`, `2.1.0`).
