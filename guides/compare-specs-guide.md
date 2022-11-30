## Comparing Specification Files Across Versions

From the API Insights dashboard, you can compare two versions of a specification file that has already been uploaded to the service:

1. In the Dashboard, select the API that has two specification files that you want to compare.
1. In the left-hand navigation bar, click **Comparison**.
1. Select the versions that you would like to compare in the two fields.
1. Click the **Compare specs** button. The system displays **"Loading..."** while making the comparison, which could take some time depending on the size of the spec files and the amount of differences. 

You can also use the CLI to compare spec files, if you have the ID values of the specification files already analyzed with the API Insights service. You can also compare a local specification file to a file already available in the API Insights service.

1. Install the API Insights CLI. You can install the CLI for local use or for use in your CICD pipeline, such as with GitHub Actions. For more information, see [API Insights CLI (api-insights-cli) Overview](../references/clidocs/api-insights-cli.md).
2. Put a copy of your `openapi.json` specification file in the directory in which you want to analyze it.
3. Run the following to compare the local spec file with the latest version available in the API Insights service. In the following, `myService` is the name of the service you set up to track the spec files.

```shell
   `api-insights-cli diff openapi.json --config .api-insights-cli.yml --service myService --latest`
```
