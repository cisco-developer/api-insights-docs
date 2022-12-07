## Create a Changelog File for API Spec Files 

<!--Check for file name changes-->

API Insights can generate a changelog that shows the differences between two revisions of a specification.

## Generating a Changelog Using the API Insights CLI

You can generate four different types of output for the changelog: text, HTML, Markdown, or JSON. By default, the CLI outputs text to the command line.

1. Install the API Insights CLI. For more information, see [API Insights CLI (api-insights-cli) Overview](../references/clidocs/api-insights-cli.md).
1. Run the following to create a Markdown changelog file based on the differences between two specification versions, where `sockshop` is the name of the service that you set up to track the spec files:

```shell
api-insights-cli diff openapi.json --config .api-insights-cli.yml --service sockshop --latest --output markdown
```

1. Run the following to generate Markdown output that shows the difference between two revisions of the specification:

```shell
api-insights-cli diff openapi.json --config .api-insights-cli.yml --service sockshop --version 0.0.1 --revision 1 --output markdown
```

## Generating a Changelog Using the API Insights Dashboard

1. In the API Insights Dashboard UI, select the API for which you would like to generate a changelog.

1. From the Details page, select the **Comparison** tab in the left navigation bar.

   ![](/images/dashboard-comparison-tab.PNG)

1. In the top header bar, select two revisions of the API spec file that you want to compare.

   ![](/images/dashboard-comparison-selection.PNG)

1. Click the **Compare Specs** button to generate the changelog.

1. API Insights displays the report in two different formats in the Dashboard UI. You can switch between them using the **Comparing** and **Markdown** tabs.

   ![](/images/dashboard-comparison-formatting-tabs.PNG)

   1. **Comparing** displays the differences between the revisions in an interactive list. You can expand some items in the list, such as entries for `Modified` items, to view a more details breakdown of the changes. Click the **Code Diff** button in an expanded report item to view the lines of code that changed.
   1. **Markdown** displays the differences between the revisions in a noninteractive list that is formatted in Markdown. Click the **Download changelog** button to download the report in Markdown format.