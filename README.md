# Curie Institute - Data Factory - Helm Charts Repository

![https://curie.fr/themes/custom/curie/images/curie-logo.png](https://curie.fr/themes/custom/curie/images/curie-logo.png)

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![(https://github.com/curie-data-factory/helm-charts/workflows/Release%20Charts/badge.svg?branch=master)](https://github.com//curie-data-factory/helm-charts/actions)
[![Artifact HUB](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/curie-df-helm-charts)](https://artifacthub.io/packages/search?repo=curie-df-helm-charts)

Welcome to the Data Factory - Curie Institute's charts repository. All charts are in the charts directory.

## Adding the chart Repository

```bash
helm repo add curiedfcharts https://curie-data-factory.github.io/helm-charts
helm repo update
```

## Contributing

Feel free to fork our repo and create a pull request with any new features or bug fixes.

## Contacting us

For issues or concerns, please fill out an issue or email us at data.factory@curie.fr

## How It Works

GitHub Pages points to the `gh-pages` branch so anything pushed to that branch will be publicly available. We are using a couple github actions to automate testing and deployment of charts. It is based off the example [here](https://github.com/helm/charts-repo-actions-demo).

## Process to add a chart to the repository

1. Create a branch or fork for your new chart
1. Initialize new chart in the `charts` directory with `helm create mychart` or by copying in your work from outside
1. After chart development is done, run (at minimum) `helm lint mychart/` to validate yaml and templates
1. Don't forget to bump your chart version (if needed)
1. Create a pull request with the new chart or updates
1. Once the PR is approved, the automation will publish the chart to our repository

## Notes about current testing

Testing is currently done with Helm3

## License

[MIT License](./LICENSE).
