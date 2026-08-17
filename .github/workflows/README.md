# GitHub Actions Workflows

Two workflows keep the Midnight Breeze theme building and shipping.

| Workflow                           | Trigger                                    | What it does                                        |
| ---------------------------------- | ------------------------------------------ | --------------------------------------------------- |
| [`test-build.yml`](test-build.yml) | every push and PR to `main`/`develop`      | validates the manifest and theme JSON, packages it  |
| [`publish.yml`](publish.yml)       | push to `main`, `v*` tags, manual dispatch | publishes to the marketplace, tags, creates release |

## How publishing works

The marketplace is the source of truth. On every run the workflow reads the
version from `package.json`, asks the marketplace whether that version already
exists, and **only publishes when it does not**. That makes every trigger safe
to fire more than once — pushing a commit and a tag together cannot publish
twice.

There are three ways to release:

### 1. Bump the version and push (simplest)

```bash
# edit "version" in package.json, then
git commit -am "chore: release 5.0.1"
git push origin main
```

The workflow publishes, creates the `v5.0.1` tag, and opens a GitHub Release
with the VSIX attached.

### 2. Use a tag

```bash
npm version patch   # bumps package.json, commits and creates the tag
git push origin main --tags
```

The workflow refuses to run if the tag and `package.json` disagree, so a
mistyped tag fails loudly instead of publishing the wrong version.

### 3. Manually

**Actions → Publish to VS Code Marketplace → Run workflow.** Tick `dry_run` to
package and validate everything without publishing.

## Release notes

Notes are taken from the matching `### <version>` section of
[`CHANGELOG.md`](../../CHANGELOG.md). Add a section for the version before
releasing, otherwise the release gets a generic one-line note.

## Setup

Publishing needs one repository secret, `VSCE_PAT`. See
[`SETUP.md`](../SETUP.md) for how to create it.

## Troubleshooting

| Symptom                               | Cause                                                               |
| ------------------------------------- | ------------------------------------------------------------------- |
| Run finishes with "Skipped"           | The version in `package.json` is already published — bump it        |
| `VSCE_PAT secret is not configured`   | The secret is missing in Settings → Secrets and variables → Actions |
| `verify-pat` fails                    | Token expired, or missing **Marketplace → Manage** scope            |
| `Tag ... does not match package.json` | Retag, or bump `package.json` to match the tag                      |
