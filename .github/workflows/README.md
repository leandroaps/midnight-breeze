# GitHub Actions Workflow for Publishing

This workflow automatically publishes the Midnight Breeze theme to the VS Code Marketplace.

## Setup Instructions

### 1. Create a Personal Access Token (PAT)

1. Go to [Azure DevOps](https://dev.azure.com/)
2. Sign in with your Microsoft account (same account used for VS Code Marketplace)
3. Click on your profile icon → **Security** → **Personal access tokens**
4. Click **+ New Token**
5. Configure the token:
   - **Name**: `vscode-marketplace-publish` (or any descriptive name)
   - **Organization**: Select **All accessible organizations**
   - **Expiration**: Choose your preferred duration (90 days, 1 year, or custom)
   - **Scopes**: Click **Show all scopes** and select:
     - ✅ **Marketplace** → **Manage** (this gives publish permissions)
6. Click **Create**
7. **IMPORTANT**: Copy the token immediately - you won't be able to see it again!

### 2. Add the Token to GitHub Secrets

1. Go to your GitHub repository: `https://github.com/leandroaps/midnight-breeze`
2. Navigate to **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**
4. Add the secret:
   - **Name**: `VSCE_PAT`
   - **Secret**: Paste the Personal Access Token you created
5. Click **Add secret**

### 3. Publishing the Theme

The workflow can be triggered in two ways:

#### Option A: Automatic Publishing (Recommended)

Create and push a version tag:

```bash
# Update version in package.json first
npm version patch  # or minor, or major

# Push the tag to GitHub
git push origin --tags
```

#### Option B: Manual Publishing

1. Go to **Actions** tab in your GitHub repository
2. Select **Publish to VS Code Marketplace** workflow
3. Click **Run workflow**
4. Select the branch and click **Run workflow**

## Workflow Details

The workflow performs the following steps:

1. Checks out the repository code
2. Sets up Node.js environment
3. Installs dependencies
4. Packages the extension using `vsce package`
5. Publishes to VS Code Marketplace using `vsce publish`

## Troubleshooting

### Authentication Failed

- Verify that `VSCE_PAT` secret is correctly set in GitHub
- Check if your Personal Access Token has expired
- Ensure the token has **Marketplace → Manage** permissions

### Package Build Failed

- Check that all required files are present
- Verify `package.json` is valid
- Ensure `@vscode/vsce` is in devDependencies

### Version Already Exists

- Update the version in [`package.json`](../../package.json:5) before publishing
- Each publish requires a unique version number

## Additional Resources

- [VS Code Publishing Extensions](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)
- [vsce CLI Documentation](https://github.com/microsoft/vscode-vsce)
- [Azure DevOps PAT Documentation](https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate)
