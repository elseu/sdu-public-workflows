# sdu-public-workflows
Collection of shared workflows

This repository holds a collection of workflows that can be used by other repositories.

⚠️ This repository is public - so be careful to not include any secrets or anything in here!

To use a workflow, include it in the `.github/workflows/*.yml` file like described in the [docs](https://docs.github.com/en/actions/using-workflows/reusing-workflows#creating-a-reusable-workflow)

### Example:
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
