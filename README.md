> ⚠️ Kargo Render and its GitHub Action are no longer maintained.
>
> Kargo Render was extracted from [Kargo](https://github.com/akuity/kargo)
> when it was a younger project in order to make parts of it having to do with
> the well-proven rendered branches pattern more immediately accessible, without
> requiring users to buy into a larger body of more experimental concepts. Since
> that time, Kargo has matured significantly, and since prior to its GA release,
> its robust support for the rendered branches pattern no longer relies on Kargo
> Render. At this time, Kargo's maintainers are confident that anything that
> could be done with Kargo Render can now be done better by Kargo itself.
>
> If you are among those who found Kargo Render to be useful, we invite you to
> now consider using [Kargo](https://github.com/akuity/kargo) instead.

---

# Kargo Render for GitHub Actions

<img width="140" align="left" src="kargo-logo.png" style="margin-right: 20px"/>

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

permissions: 
  contents: write
  pull-requests: write # Optional, depending on your workflow

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
      uses: akuity/kargo-render-action@v0.1.0-rc.42
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
