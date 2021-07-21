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
- Iterates the prerelease version using `--canary` arg that allows prerelease (not necessarily canary) https://github.com/lerna/lerna/tree/main/commands/publish#--canary https://github.com/lerna/lerna/tree/main/commands/publish#--preid

ideally: 

Changes:
 - @JackHowa/headline: 1.1.1 => 1.1.1-canary.1
 - @JackHowa/sub-headline (no change)

lerna info versioning independent

successful: 

lerna info ci enabled
lerna info canary enabled
lerna info Looking for changed packages since 119e029^..119e029
lerna info ignoring diff in paths matching [ 'ignored-file', '*.md' ]
Found 1 package to publish:
 - @JackHowa/headline => 1.2.3-canary.14+119e029

lerna info auto-confirmed 
lerna info publish Publishing packages to npm...
lerna notice Skipping all user and access validation due to third-party registry
lerna notice Make sure you're authenticated properly ¯\_(ツ)_/¯
lerna http fetch PUT 200 https://npm.pkg.github.com/@JackHowa%2fheadline 1472ms
lerna success published @JackHowa/headline 1.2.3-canary.14+119e029
lerna notice 
lerna notice 📦  @JackHowa/headline@1.2.3-canary.14+119e029
lerna notice === Tarball Contents === 
lerna notice 1.1kB LICENSE     
lerna notice 122B  index.js    
lerna notice 537B  package.json
lerna notice 3.3kB CHANGELOG.md
lerna notice === Tarball Details === 
lerna notice name:          @JackHowa/headline                           
lerna notice version:       1.2.3-canary.14+119e029                      
lerna notice filename:      JackHowa-headline-1.2.3-canary.14+119e029.tgz
lerna notice package size:  1.9 kB                                       
lerna notice unpacked size: 5.0 kB                                       
lerna notice shasum:        283eb794d59e3cd28235afe7c909b31b551a2d7b     
lerna notice integrity:     sha512-r1GL66ZYcZBVJ[...]21UvEiaAxQDWg==     
lerna notice total files:   4                                            
lerna notice 
Successfully published:
 - @JackHowa/headline@1.2.3-canary.14+119e029
lerna success published 1 package


### `npm run lerna-version`

- Increment version via lerna https://github.com/lerna/lerna/tree/main/commands/version
- Can't override `npm run version` as it's `lerna ERR! lifecycle "version" errored in "lerna-monorepo-practice", exiting 1`

### `npm run lerna-version:canary`

UPDATE: this is not what we want. This does not publish to canary tag (https://github.com/JackHowa/lerna-monorepo-components/runs/3125908320?check_suite_focus=true)

- Increment the prerelease version once forward with canary ahead of `release:canary`
- note: `If you have any packages with a prerelease version number (e.g. 2.0.0-beta.3) and you run lerna version with and a non-prerelease bump (major, minor, or patch), it will publish those previously pre-released packages as well as the packages that have changed since the last release.` https://github.com/lerna/lerna/tree/main/commands/version#prerelease
# References 

- Fetch depth lerna issue https://stackoverflow.com/a/60184319/7491536
- Lerna getting started https://github.com/lerna/lerna#getting-started
- npmrc within the GitHub Action to push and pull https://viewsource.io/publishing-and-installing-private-github-packages-using-yarn-and-lerna/