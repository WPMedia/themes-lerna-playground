# lerna-monorepo-components

[![lerna](https://img.shields.io/badge/maintained%20with-lerna-cc00ff.svg)](https://lerna.js.org/)

Published here https://www.npmjs.com/package/@thrash-industries/headline 

Goals: 

- [x] Publish to GitHub Packages https://github.com/JackHowa?tab=packages&repo_name=lerna-monorepo-components
- [x] Use fixed version for default publish https://github.com/JackHowa/lerna-monorepo-components/blob/main/lerna.json#L5
- [x] Publish all for one branch `stable` to `stable` tag https://github.com/JackHowa/lerna-monorepo-components/runs/3118218953?check_suite_focus=true
- [ ] Publish really anything (including stable) independently?
- [ ] Only publish on changes for one branch `canary`. Using version independent


Want the iteration of version to in the lerna.json to change upon GitHub Action publish.

It seems like --git-tag-no-push can cause problems.

## scripts 

### `npm run release`

- Full release

### `npm run release:force`

- Force release all packages regardless of changes
- This can happen if there's a botched release
### `npm run release:stable`

- Only publish packages to stable tag
- Force publish all packages regardless of changes

### `npm run release:canary`

- Only publish packages to canary tag
- Publish packages based on only changes

ideally: 

Changes:
 - @JackHowa/headline: 1.1.1 => 1.1.1-canary.1
 - @JackHowa/sub-headline (no change)
### `npm run lerna-version`

- Increment version via lerna https://github.com/lerna/lerna/tree/main/commands/version
- Can't override `npm run version` as it's `lerna ERR! lifecycle "version" errored in "lerna-monorepo-practice", exiting 1`