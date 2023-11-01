# actions-release-ui-components
## Description
Releases UI components using shared release manifest

## Requirements
- [Checkout](https://github.com/actions/checkout) - to clone the repo

## Environment Variables/Secrets

| Env Var/Secret | Desription | Required |
|-------|------------|----------|
| NPM_RELEASE_TOKEN | Secret/Env Var containing the NPM token used for releases. | true |

## Usage
```yaml
name: Release
on: [ main ]
jobs:
  release_component:
    name: Release
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: prefecthq/actions-release-ui-components@main
        with:
          NPM_TOKEN: ${{ secrets.NPM_TOKEN_SUPER_SECRET }}
```