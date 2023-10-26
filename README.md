# Trusted Artifact Signer Github actions  
This repository hosts all reusable GitHub actions utilized by the 'securesign' organization on GitHub.

## Current list of actions
The current actions included in this repository include:

### Check image version
This GitHub Action utilizes skopeo to verify that the images ubi9/go-toolset and ubi9/ubi-minimal are always using the most up-to-date SHA. If they aren't, the action will create a PR to update them in any of the branches specified in the matrix.

#### Usage

```    
check-image-version:
  uses: securesign/actions/.github/workflows/check-image-version.yaml@main
  strategy:
    matrix:
      branch: [main, midstream-vx-y-z, ....]
  with:
    branch: ${{ matrix.branch }}
  secrets:
    token: ${{ secrets.GITHUB_TOKEN }}
```

In order for the action to work correctly there are two settings that need to be changed for the repo.

1. Actions need to be able to create pull requests (settings -> Actions -> General -> Workflow permissions)
2. Actions need read and write permissions (settings -> Actions -> General -> Workflow permissions)

# Contributing
If you want to add a reusable GitHub action, please refer to the documentation [here](https://docs.github.com/en/actions/using-workflows/reusing-workflows).
