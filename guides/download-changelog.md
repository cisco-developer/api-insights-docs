## Create a Changelog File for API Spec Files 

<!--Check for file name changes-->

API Insights can You can get four different types of output for the changelog: text, HTML, Markdown, or JSON. By default, the CLI outputs text to the command line.

1. Install the API Insights CLI. For more information, see [API Insights CLI (api-insights-cli) Overview](../references/clidocs/api-insights-cli.md).
1. Run the following to create a Markdown changelog file based on the differences between two specification versions, where `sockshop` is the name of the service that you set up to track the spec files:

```shell
api-insights-cli diff openapi.json --config .api-insights-cli.yml --service sockshop --latest --output markdown
```

1. Run the following to generate Markdown output that shows the difference between two revisions of the specification:

```shell
api-insights-cli diff openapi.json --config .api-insights-cli.yml --service sockshop --version 0.0.1 --revision 1 --output markdown
```

   By default, the CLI tool outputs text. 