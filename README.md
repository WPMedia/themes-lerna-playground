# lerna-monorepo-components

[![lerna](https://img.shields.io/badge/maintained%20with-lerna-cc00ff.svg)](https://lerna.js.org/)

Published here https://www.npmjs.com/package/@thrash-industries/headline 

Goals: 

- [x] Publish to GitHub Packages https://github.com/JackHowa?tab=packages&repo_name=lerna-monorepo-components
- [x] Use fixed version for default publish https://github.com/JackHowa/lerna-monorepo-components/blob/main/lerna.json#L5
- [x] Publish all for one branch `stable` to `stable` tag https://github.com/JackHowa/lerna-monorepo-components/runs/3118218953?check_suite_focus=true
- [ ] Publish really anything (including stable) independently?
- [ ] Only publish on changes for one branch `canary`. Using version independent. 
- [ ] Make sure that we can still push to the branch https://github.community/t/allowing-github-actions-bot-to-push-to-protected-branch/16536/5

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

 Still seeing: 

https://github.com/JackHowa/lerna-monorepo-components/runs/3124889448?check_suite_focus=true 

 ```
lerna notice cli v4.0.0
lerna info versioning independent
lerna info ci enabled
lerna info Looking for changed packages since @JackHowa/headline@1.2.0
lerna info ignoring diff in paths matching [ 'ignored-file', '*.md' ]
lerna info getChangelogConfig Successfully resolved preset "conventional-changelog-angular"
lerna info auto-confirmed 

 ```

 now seeing (no changes): 

 ```
Run npm run release:canary
  npm run release:canary
  shell: /usr/bin/bash -e {0}
  env:
    NODE_AUTH_TOKEN: ***

> lerna-monorepo-practice@1.0.0 release:canary /home/runner/work/lerna-monorepo-components/lerna-monorepo-components
> lerna publish --dist-tag canary -y

lerna notice cli v4.0.0
lerna info versioning independent
lerna info ci enabled
lerna info Looking for changed packages since @JackHowa/headline@1.2.2
lerna info ignoring diff in paths matching [ 'ignored-file', '*.md' ]
lerna success No changed packages to publish 

 ```


 only change of one package (https://github.com/JackHowa/lerna-monorepo-components/runs/3124961701?check_suite_focus=true):

```

Changes:
lerna info auto-confirmed 
 - @JackHowa/headline: 1.2.2 => 1.2.3

```

ideally: should be a prerelease with a canary tag

### `npm run lerna-version`

- Increment version via lerna https://github.com/lerna/lerna/tree/main/commands/version
- Can't override `npm run version` as it's `lerna ERR! lifecycle "version" errored in "lerna-monorepo-practice", exiting 1`

### `npm run lerna-version:canary`

- Increment the prerelease version once forward with canary ahead of `release:canary`
- note: `If you have any packages with a prerelease version number (e.g. 2.0.0-beta.3) and you run lerna version with and a non-prerelease bump (major, minor, or patch), it will publish those previously pre-released packages as well as the packages that have changed since the last release.` https://github.com/lerna/lerna/tree/main/commands/version#prerelease
# References 

- Fetch depth lerna issue https://stackoverflow.com/a/60184319/7491536
- Lerna getting started https://github.com/lerna/lerna#getting-started
- npmrc within the GitHub Action to push and pull https://viewsource.io/publishing-and-installing-private-github-packages-using-yarn-and-lerna/