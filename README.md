# Trusted Artifact Signer Github actions  
This repository hosts all reusable GitHub actions utilized by the 'securesign' organization on GitHub.

## Current list of actions
The current actions included in this repository include:

### Check image version
This GitHub Action utilizes skopeo to verify that the images specified in the inputs, are always using the most up-to-date SHA. If they aren't, the action will create a PR to update them in any of the branches specified in the matrix.

#### Usage

```    
check-image-version:
  uses: securesign/actions/.github/workflows/check-image-version.yaml@main
  strategy:
    matrix:
      branch: [main, midstream-vx-y-z, ....]
    with:
      branch: ${{ matrix.branch }}
      images: '["img1","img2","img3","img4"]'
    secrets:
      token: ${{ secrets.GITHUB_TOKEN }}
      registry_redhat_io_username: ${{ secrets.REGISTRY_REDHAT_IO_USERNAME }}
      registry_redhat_io_password: ${{ secrets.REGISTRY_REDHAT_IO_PASSWORD }}
```

In order for the action to work correctly there are two settings that need to be changed for the repo.

1. Actions need to be able to create pull requests (settings -> Actions -> General -> Workflow permissions)
2. Actions need read and write permissions (settings -> Actions -> General -> Workflow permissions)

### Trigger konflux build
This Github action opens a pr with a timestamp file, with the aim of easily triggering a build on Konflux. (May need to add the file to cel expressions in the tekton pipelines)

### Usage
```
name: Trigger Konflux build
on:
  workflow_dispatch:

jobs:
  trigger-konflux-build:
    uses: securesign/actions/.github/workflows/trigger-konflux-build.yaml@main
    with:
      branch: main
    secrets:
      token: ${{ secrets.GITHUB_TOKEN }}
```

In order for the action to work correctly there are two settings that need to be changed for the repo.

1. Actions need to be able to create pull requests (settings -> Actions -> General -> Workflow permissions)
2. Actions need read and write permissions (settings -> Actions -> General -> Workflow permissions)

# Contributing
If you want to add a reusable GitHub action, please refer to the documentation [here](https://docs.github.com/en/actions/using-workflows/reusing-workflows).
