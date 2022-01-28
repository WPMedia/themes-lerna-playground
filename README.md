# lerna-monorepo-components

[![lerna](https://img.shields.io/badge/maintained%20with-lerna-cc00ff.svg)](https://lerna.js.org/)

Published here https://www.npmjs.com/package/@thrash-industries/headline 

Goals: 

- [x] Publish to GitHub Packages https://github.com/JackHowa?tab=packages&repo_name=lerna-monorepo-components
- [x] Use fixed version for default publish https://github.com/JackHowa/lerna-monorepo-components/blob/main/lerna.json#L5
- [x] Publish all for one branch `stable` to `stable` tag https://github.com/JackHowa/lerna-monorepo-components/runs/3118218953?check_suite_focus=true
- [x] Publish really anything (including stable) independently?
- [x] Only publish on changes for one branch `canary`. Using version independent. 
- [x] Make sure that we can still push to the branch https://github.community/t/allowing-github-actions-bot-to-push-to-protected-branch/16536/5 https://github.com/JackHowa/lerna-monorepo-components/runs/3126482038?check_suite_focus=true with push settings
- [x] On merging stable back to canary, we should ignore changes to package.json. Otherwise, all changed blocks will need to be republished to canary again and the cycle will go on and on. yes! https://github.com/JackHowa/lerna-monorepo-components/runs/3126310013?check_suite_focus=true
- [ ] If merging into another branch, the approver needs to have write access. But this doesn't seem to be toggleable inside of a non-org repo. https://github.com/JackHowa/lerna-monorepo-components/runs/3126597880?check_suite_focus=true https://github.com/JackHowa/lerna-monorepo-components/pull/6


## scripts 


### `npm run release:stable`

- Only publish packages to stable tag
- "release:stable": "lerna publish --dist-tag stable -y", better because no force publishes and only changed ones 
- ideally should go from: (done https://github.com/JackHowa/lerna-monorepo-components/runs/3126215436?check_suite_focus=true)

 - @JackHowa/headline: 1.2.5-canary.0 => 1.2.6

### `npm run release:canary`

- Only publish packages to canary tag
- Publish packages based on only changes
- Iterates the prerelease version using `--canary` arg that allows prerelease (not necessarily canary) https://github.com/lerna/lerna/tree/main/commands/publish#--canary https://github.com/lerna/lerna/tree/main/commands/publish#--preid

Changes:
 - @JackHowa/headline: 1.1.1 => 1.1.1-canary.1
 - @JackHowa/sub-headline (no change)



# References 

- Fetch depth lerna issue https://stackoverflow.com/a/60184319/7491536
- Lerna getting started https://github.com/lerna/lerna#getting-started
- npmrc within the GitHub Action to push and pull https://viewsource.io/publishing-and-installing-private-github-packages-using-yarn-and-lerna/
