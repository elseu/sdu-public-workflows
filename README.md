# sdu-public-workflows
Collection of shared workflows

This repository holds a collection of workflows that can be used by other repositories.

⚠️ This repository is public - so be careful to not include any secrets or anything in here!

### Workflows
To use a workflow, include it in the `.github/workflows/*.yml` file like described in the [docs](https://docs.github.com/en/actions/using-workflows/reusing-workflows#creating-a-reusable-workflow)

For example:

_.github/workflows/sync.yml_
```yaml
name: Sync main to develop

on:
  push:
    branches:
      - main

jobs:
  sync-branches:
    uses: elseu/sdu-public-workflows/.github/workflows/sync-main-to-develop.yml@main
    secrets: inherit
```

### Actions
To use an action, include it in the `.github/workflows/*.yml` file like described in the [docs](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action#testing-out-your-action-in-a-workflow)

Be aware that you have to provide the correct input, in the example below it's the `npm_token` - secrets can't be passed along to composite actions!

For example:

_.github/workflows/install-and-deploy.yml_
```yaml
name: Sync build and deploy 

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      # npm install
      - uses: elseu/sdu-public-workflows/.github/actions/npm-install
        with:
          npm_token: ${{ secrets.SDU_READ_PACKAGES_GH_PAT }}

      - name: NPM build
        run: npm run build
      - name: NPM build storybook
        run: npm run build-storybook
```
