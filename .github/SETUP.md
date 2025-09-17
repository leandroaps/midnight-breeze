# GitHub Actions Setup for VS Code Extension Publishing

This repository includes GitHub Actions that automatically build and publish your VS Code theme to the Visual Studio Code Marketplace.

## 🚨 Important: Authentication Issues Fixed

If you're experiencing authentication failures with VSCE_PAT, please see:

- [`GITHUB_ACTIONS_FIXES.md`](../GITHUB_ACTIONS_FIXES.md) - Complete workflow improvements
- [`VSCE_PAT_TROUBLESHOOTING.md`](../VSCE_PAT_TROUBLESHOOTING.md) - Step-by-step troubleshooting

## Prerequisites

### 1. Visual Studio Code Marketplace Publisher Account

1. Go to [Visual Studio Marketplace Publisher Management](https://marketplace.visualstudio.com/manage)
2. Sign in with your Microsoft account
3. Create a publisher account if you don't have one
4. **Critical**: Ensure the publisher name exactly matches the `publisher` field in your `package.json`

**Current Configuration Check:**

```json
// In your package.json
{
  "publisher": "leandroaps" // Must match marketplace publisher exactly
}
```

### 2. Personal Access Token (PAT) - Updated Process

1. Go to [Azure DevOps](https://dev.azure.com)
2. Sign in with the **exact same Microsoft account** used for the marketplace
3. Click your profile picture → **User settings** → **Personal access tokens**
4. Click **+ New Token**
5. Configure the token:
   - **Name**: `VSCode Extension Publishing - 2024`
   - **Organization**: Select your organization (or "All accessible organizations")
   - **Expiration**: 1 year (recommended)
   - **Scopes**: Select **Custom defined** and check:
     - ✅ **Marketplace** → **Manage**
6. Click **Create** and **copy the token immediately** (you won't see it again!)

### 3. GitHub Repository Secrets

1. Go to your GitHub repository
2. Click **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**
4. Add the following secret:
   - **Name**: `VSCE_PAT`
   - **Value**: The Personal Access Token you created above

### 4. Verify Your Setup

Test your configuration locally before using GitHub Actions:

```bash
# Install VSCE globally
npm install -g @vscode/vsce

# Test authentication (replace YOUR_TOKEN with actual token)
vsce verify-pat YOUR_TOKEN

# Test packaging
vsce package

# Test publish (dry run - won't actually publish)
vsce publish --dry-run --pat YOUR_TOKEN
```

## How to Use

### 🚀 Automatic Publishing (Recommended)

1. **Update version in `package.json`**:

   ```bash
   npm version patch  # for bug fixes (3.0.1 → 3.0.2)
   npm version minor  # for new features (3.0.1 → 3.1.0)
   npm version major  # for breaking changes (3.0.1 → 4.0.0)
   ```

2. **Commit and create tag**:

   ```bash
   git add package.json
   git commit -m "Bump version to $(node -p 'require(\"./package.json\").version')"
   git tag v$(node -p 'require("./package.json").version')
   git push origin main --tags
   ```

3. **The GitHub Action will automatically**:
   - ✅ Validate authentication and configuration
   - ✅ Build and package the extension
   - ✅ Publish to VS Code Marketplace
   - ✅ Create a GitHub release with detailed notes
   - ✅ Upload the VSIX file as a release asset

### 🔧 Manual Publishing (Testing)

1. Go to your repository on GitHub
2. Click **Actions** → **Publish VS Code Extension**
3. Click **Run workflow**
4. Enter the version number (e.g., `3.0.2`)
5. Click **Run workflow**

**Note**: Use manual publishing for testing the workflow before doing automatic releases.

## 🔍 Workflow Features (Enhanced)

- ✅ **Authentication validation** - Tests VSCE_PAT before publishing
- ✅ **Publisher verification** - Confirms package.json matches marketplace
- ✅ **Automatic building and packaging** - Creates VSIX files
- ✅ **Marketplace publishing** - Uploads to VS Code Marketplace
- ✅ **GitHub releases** - Creates releases with detailed notes
- ✅ **Artifact management** - Stores VSIX files with version tracking
- ✅ **Error handling** - Comprehensive logging and validation
- ✅ **Modern actions** - Uses latest GitHub Actions (no deprecated ones)

## 🐛 Troubleshooting

### Quick Fixes for Common Issues

1. **"Publisher not found"** → Check [`VSCE_PAT_TROUBLESHOOTING.md`](../VSCE_PAT_TROUBLESHOOTING.md#error-publisher-xyz-not-found)
2. **"Authentication failed"** → See [PAT recreation guide](../VSCE_PAT_TROUBLESHOOTING.md#step-by-step-pat-recreation)
3. **"Version already exists"** → Increment version in `package.json`
4. **Workflow fails** → Check [detailed troubleshooting guide](../GITHUB_ACTIONS_FIXES.md#troubleshooting-common-issues)

### 📋 Pre-Publishing Checklist

Before publishing, verify:

- [ ] `package.json` publisher matches marketplace publisher exactly
- [ ] Version number is incremented
- [ ] VSCE_PAT secret is set in GitHub repository
- [ ] Theme file is valid JSON
- [ ] All required package.json fields are present

### 🔍 Checking Workflow Logs

1. Go to **Actions** tab in your GitHub repository
2. Click on the failed workflow run
3. Expand each step to see detailed logs
4. Look for specific error messages and match them with troubleshooting guides

## 📊 Version Management

### Supported Versioning Methods

1. **Git Tags** (Automatic): Version extracted from git tag (e.g., `v3.0.2`)
2. **Manual Input**: Version specified when manually triggering workflow
3. **NPM Commands**: Use `npm version` for automatic version bumping

### Version Format Requirements

- Must follow semantic versioning: `MAJOR.MINOR.PATCH`
- Examples: `1.0.0`, `2.1.3`, `10.0.1`
- Git tags should be prefixed with `v`: `v1.0.0`

## 🆘 Need Help?

1. **Authentication Issues**: [`VSCE_PAT_TROUBLESHOOTING.md`](../VSCE_PAT_TROUBLESHOOTING.md)
2. **Workflow Problems**: [`GITHUB_ACTIONS_FIXES.md`](../GITHUB_ACTIONS_FIXES.md)
3. **Local Testing**: Run `vsce package` and `vsce verify-pat YOUR_TOKEN`
4. **GitHub Issues**: Create an issue in this repository with workflow logs
