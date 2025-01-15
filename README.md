# actions-release-ui-components
## Description
Releases UI components using shared release manifest

## Requirements
- [Checkout](https://github.com/actions/checkout) - to clone the repo

## Environment Variables/Secrets

| Env Var/Secret | Desription | Required |
|-------|------------|----------|
| GITHUB_TOKEN | Secret/Env Var containing the Github token used for releases. (It is the default git token) | true |
| NPM_RELEASE_TOKEN | Secret/Env Var containing the NPM token used for releases. | true |
| RELEASE_TYPE | The type of release to perform. (major, minor, patch) | true |
| SKIP_BUILD | Bool for whether or not to skip the build step (req by eslint-config). | false |
| WORKING_DIR | Directory containing the package to build and release. Defaults to repository root ('.') | false |

## Usage
```yaml
name: Release
on:
  workflow_dispatch:
    inputs:
      release_type:
        description: Type of release to perform
        required: true
        default: patch
jobs:
  release_component:
    name: Release
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

    - name: Configure git user
      run: |
        git config user.name "$GITHUB_ACTOR"
        git config user.email "$GITHUB_ACTOR@users.noreply.github.com"

      - uses: prefecthq/actions-release-ui-components@main
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          RELEASE_TYPE: ${{ inputs.release_type }}
          NPM_TOKEN: ${{ secrets.NPM_TOKEN_SUPER_SECRET }}
          WORKING_DIR: 'packages/ui-components' # Optional: specify a different working directory
```