# lerna-monorepo-components

[![lerna](https://img.shields.io/badge/maintained%20with-lerna-cc00ff.svg)](https://lerna.js.org/)

## scripts 

### `npm run release`

- Full release

### `npm run release:force`

- Force release all packages regardless of changes
- This can happen if there's a botched release
### `npm run lerna-version`

- Increment version via lerna https://github.com/lerna/lerna/tree/main/commands/version
- Can't override `npm run version` as it's `lerna ERR! lifecycle "version" errored in "lerna-monorepo-practice", exiting 1`