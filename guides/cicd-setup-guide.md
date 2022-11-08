# Setting Up API Insights in a CI/CD Pipeline 

The instructions in this section walk you through configuring API Insights to run as part of your GitHub CI/CD pipeline. When you commit a new version of your spec file to your repository with an appropriate release tag, the API Insights analyzers run as GitHub actions. The results of the analysis, along with the spec file itself, are then uploaded to the API Insights remote service.

## Creating the Config File

To get started, create an `api-insights.yaml` file in your repository's `.github/workflows` directory. This file contains the environment variables which API Insights uses, as well as the logic for its analyzers. You can use the following sample YAML file to get started, and customize its `run` commands to suit your needs:

```yaml
name: API Insights

on:
  push:
    branches:
      - "*"
    tags: [v*.*.*-*]

env:
  API_INSIGHTS_CLI_VERSION: latest
  RELEASE_REVISON: 10

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # analyze API spec files
  # by default, the analysis fails if any issues are found that have the "Error" severity category
  # You can also use `--fail-below-score int` to cause analyzers to fail with the specified minimal target score.
  analyze:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: API Insights - Install CLI
        uses: supplypike/setup-bin@v1
        with:
          uri: ${{ env.API_INSIGHTS_CLI_DOWNLOAD_URL }}
          name: ${{ env.API_INSIGHTS_CLI_NAME }}
          version: ${{ env.API_INSIGHTS_CLI_VERSION }}
      - name: API Insights - Analyze API Spec
        run: |
          api-insights-cli analyze ${{ env.API_SPEC }} --fail-below-score 80 --host ${{ env.API_INSIGHTS_HOST }} --base-path ${{ env.API_INSIGHTS_BASE_PATH }}
  diff:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: API Insights - Install CLI
        uses: supplypike/setup-bin@v1
        with:
          uri: ${{ env.API_INSIGHTS_CLI_DOWNLOAD_URL }}
          name: ${{ env.API_INSIGHTS_CLI_NAME }}
          version: ${{ env.API_INSIGHTS_CLI_VERSION }}
      - name: API Insights - Diff API SPec
        run: |
          api-insights-cli diff ${{ env.API_SPEC }} -s ${{ env.API_INSIGHTS_SERVICE }} --latest --fail-on-incompatible --host ${{ env.API_INSIGHTS_HOST }} --base-path ${{ env.API_INSIGHTS_BASE_PATH }}
  upload:
    # Use `needs` to define prerequisite jobs, e.g. only upload when step `analyze` and `diff` is successful.
    # needs: [ analyze, diff]
    runs-on: ubuntu-latest
    if: startsWith(github.ref, 'refs/tags/v')
    steps:
      - uses: actions/checkout@v3
      - name: API Insights - Install CLI
        uses: supplypike/setup-bin@v1
        with:
          uri: ${{ env.API_INSIGHTS_CLI_DOWNLOAD_URL }}
          name: ${{ env.API_INSIGHTS_CLI_NAME }}
          version: ${{ env.API_INSIGHTS_CLI_VERSION }}
      - name: Set tag env
        run: echo "RELEASE_TAG=${GITHUB_REF#refs/*/}" >> $GITHUB_ENV
      - id: parse-tags
        name: Parse tags
        uses: actions/github-script@v6
        with:
          script: |
            const items = "${{ env.RELEASE_TAG }}".split('-')
            console.log(items)
            core.setOutput('version', items[0])
            core.setOutput('revision', items[1])
      - name: Set version env
        run: echo "RELEASE_VERSION=${{steps.parse-tags.outputs.version}}" >> $GITHUB_ENV
      - name: Set revision env
        run: echo "RELEASE_REVISON=${{steps.parse-tags.outputs.revision}}" >> $GITHUB_ENV
      - name: API Insights - Upload API SPec
        run: |
          api-insights-cli service uploadspec ${{ env.API_SPEC }} -s ${{ env.API_INSIGHTS_SERVICE }} --revision ${{ env.RELEASE_REVISON }} --host ${{ env.API_INSIGHTS_HOST }} --base-path ${{ env.API_INSIGHTS_BASE_PATH }}
```

The `on` section of the YAML file indicates that the API Insights actions should run when a new version of the API spec file is released.

The `env` section contains important environment variables which you must define.

The `jobs` section defines three GitHub actions, **Upload**, **Diff**, and **Analyze**, which run API Insights CLI commands.

* The **Upload** action executes `api-insights-cli service uploadspec`.
* The **Diff** action executes `api-insights-cli diff` to compare the latest spec file version to another specified version and generates a diff report.
* The **Analyze** action executes `api-insights-cli analyze` to score the spec file against API guidelines, completeness, inclusive language, and security.

For more information about the CLI commands that these actions execute, see the (API Insights CLI Reference)[/references/clidocs/api-insights-cli.md] section.

## Triggering the API Insights CI/CD Pipeline

To trigger the pipeline, do the following:
1. Commit a new version of your spec file to the repository.
1. Use the "Create a New Release" link in GitHub to create a new release.
1. Create a new tag for the release with the version number in the format `v*.*.*-rev` where the asterisks `*` are the version number and `rev` is a descriptor for the release, such as `beta0`. API Insights parses the version tag and displays the version number and descriptor in the API Insights dashboard.
1. Check the API Insights dashboard to find the spec file and its analysis information.
