## Create a Changelog File for API Spec Files 

API Insights can produce a changelog for a particular API in four different output formats types: text, HTML, Markdown, or JSON. By default, the CLI outputs text to the command line. To generate a changelog file, do the following:

1. Install the API Insights CLI. For more information, see [API Insights CLI (api-insights-cli) Overview](../references/clidocs/api-insights-cli.md).
1. Run the following to create a changelog file in Markdown format, based on the differences between two specification versions, where `myService` is the name of the service that you set up to track the spec files:

```shell
api-insights-cli diff openapi.json --config .api-insights-cli.yml --service myService --latest --output markdown
```

1. Run the following to generate Markdown output that shows the difference between two specified revisions of the specification (here versions `0.0.1` and `1`):

```shell
api-insights-cli diff openapi.json --config .api-insights-cli.yml --service myService --version 0.0.1 --revision 1 --output markdown
```
