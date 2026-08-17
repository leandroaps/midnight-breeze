# Publishing setup

Everything the repository needs in order to publish Midnight Breeze to the
Visual Studio Code Marketplace automatically. For how the workflows behave day
to day, see [`workflows/README.md`](workflows/README.md).

## 1. Publisher account

The `publisher` field in [`package.json`](../package.json) must match a
publisher you own at
[Marketplace publisher management](https://marketplace.visualstudio.com/manage).

This repository publishes as **`leandroaps`**.

## 2. Personal Access Token

1. Go to [Azure DevOps](https://dev.azure.com) and sign in with the **same
   Microsoft account** that owns the publisher.
2. Profile picture → **User settings** → **Personal access tokens** → **New Token**.
3. Configure it:
   - **Organization**: All accessible organizations
   - **Expiration**: up to one year
   - **Scopes**: Custom defined → **Marketplace** → **Manage**
4. Create it and copy the token immediately — it is shown only once.

Tokens expire. When publishing starts failing at the `Verify VSCE_PAT` step,
this is almost always why.

## 3. Repository secret

In the GitHub repository: **Settings → Secrets and variables → Actions → New
repository secret**.

- **Name**: `VSCE_PAT`
- **Value**: the token from step 2

This is the only secret required. The workflow uses the built-in `GITHUB_TOKEN`
for tags and releases.

## 4. Verify locally (optional)

```bash
npm ci
npx vsce verify-pat leandroaps   # reads VSCE_PAT from the environment
npx vsce ls                      # shows exactly what ships in the VSIX
npm run build                    # produces the .vsix
```

`npx vsce ls` is worth a look after changing `.vscodeignore` — anything listed
there is uploaded to the marketplace.

## Releasing

Bump `version` in `package.json`, add the matching `### <version>` section to
[`CHANGELOG.md`](../CHANGELOG.md), commit and push to `main`. The workflow
publishes, tags and creates the release.

Full details and the alternative tag-based and manual flows are in
[`workflows/README.md`](workflows/README.md).

## Checklist before releasing

- [ ] `version` in `package.json` is higher than the published one
- [ ] `CHANGELOG.md` has a `### <version>` section for it
- [ ] `VSCE_PAT` secret exists and has not expired
- [ ] `npx vsce ls` shows no unwanted files
