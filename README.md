# Kargo Render for GitHub Actions

<img width="80" align="left" src="logo.png" style="right-margin: 20px"/>

Use Kargo Render for GitHub Actions along with Kustomize or Helm to pre-render
environment-specific configuration into (plain YAML) Kubernetes manifests
committed (or PR'ed) to environment-specific branches that are easily consumed
by your favorite GitOps platform.

<br clear="left"/>

🟡&nbsp;&nbsp;Both Kargo Render and its GitHub Action are highly experimental at
this time and breaking changes should be anticipated between pre-GA minor
releases.

## Getting Started

First learn about Kargo Render in our [docs](https://kargo-render.akuity.io).

Then, integrate with GitHub Actions. In this simple example, every commit to
the `main` branch results in environment-specific configuration being rendered
and written to the `env/dev`, `env/stage`, and `env/prod` branches.

```yaml
name: Commit Workflow

on:
  push:
    branches:
    - main

jobs:
  render-manifests:
    name: Render and Commit Manifests
    runs-on: ubuntu-latest
    strategy:
      matrix:
        targetBranch:
        - env/dev
        - env/stage
        - env/prod
    steps:
    - name: Render and Commit Manifests
      uses: akuity/kargo-render-by-akuity@v0.1.0-rc.32
      with:
        personalAccessToken: ${{ secrets.GITHUB_TOKEN }}
        targetBranch: ${{ matrix.targetBranch }}
```

## Contributing

Kargo Render for GitHub Actions accepts contributions via GitHub pull requests.

## Support & Feedback

To report an issue, request a feature, or ask a question, please open an issue
[here](https://github.com/akuity/kargo-render-action/issues).

## Code of Conduct

Participation in Kargo Render for GitHub Actions is governed by the
[Contributor Covenant Code of Conduct](https://kargo-render.akuity.io/contributor-guide/code-of-conduct/).
