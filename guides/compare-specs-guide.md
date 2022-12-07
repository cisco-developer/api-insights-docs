## Comparing Specification Files Across Versions

From the API Insights dashboard, you can compare two versions of a specification file that has already been uploaded to the service:

1. In the Dashboard, select the API that has two specification files that you want to compare.
1. In the left-hand side bar, click **Comparison**.
1. Select a version value, such as `1.4.0 GA` from the first "Please select" menu.
1. Select a version value, such as `1.5.0 beta 0` from the next "Please select" menu.
1. Click the **Compare specs** button. The system displays "Loading..." while making the comparison, which could take some time depending on the size of the spec files and the amount of differences. 

You can compare specification files with the CLI as well when you have the ID values of the specification files already analyzed with the API Insights service. You can also compare a local specification file to a file already available in the API Insights service.

1. Install the API Insights CLI and make sure authentication is configured properly for your API Insights service. You can install the CLI for local use or for use in your CI/CD pipeline, such as with GitHub Actions.
2. Put a copy of your `openapi.json` specification file in the directory where you want to analyze it.
3. To compare that local specification file with the latest version available in the API Insights service, you run this command, where `sockshop` is the name of the service you set up to track the spec files:

```shell
   `api-insights-cli diff openapi.json --config .api-insights-cli.yml --service sockshop --latest`
```
