# setup-helm-workspace-action
Action to setup a Helm workspace

## Usage

```yaml
  helm:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - uses: Updater/setup-helm-workspace-action@main
        id: setup
        with:
          helm-password: ${{ secrets.HARBOR_PASSWORD }}
          helm-username: ${{ secrets.HARBOR_USERNAME }}
      - uses: Updater/helm-test-action@main
        if: steps.setup.outputs.changed == 'true'
      - uses: Updater/helm-release-action@main
        if: steps.setup.outputs.changed == 'true'
        with:
          pre-release: "true"
```
