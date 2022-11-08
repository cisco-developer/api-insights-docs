<seotitle>API Insights is an open-source tool that helps developers improve API quality and security</seotitle>

# What is API Insights?

As APIs become increasingly important to many diverse organizations, the importance of good API design also grows. APIs need to be secure, consistent, usable, and inclusive. As any API grows and develops, logistical challenges also arise. New versions of an API might introduce breaking changes, which can increase development time and accumulate technical debt. Third-party APIs might be introduced and then forgotten about, lingering in an application but no longer supported. API Insights provides robust and customizable analysis tools to help you and your organization manage and overcome these API requirements and challenges.

**API Insights** helps you improve your API quality by analyzing and scoring your Swagger 2.0 or OpenAPI 3.x specification (spec) files. API Insights can perform its static analysis in your GitHub CI/CD pipeline, on your local machine through a CLI, or in Visual Studio Code as an IDE extension. API Insights also provides a browser-based dashboard, which catalogs and tracks your APIs, their versions, and their analysis scores.

API Insights runs several **analyzers** to assess and score API spec files on the following dimensions:

* **Adherence to OpenAPI Guidelines** promotes consistency across our APIs and promotes good design practices.
* **Documentation Completeness** means that an API contains descriptions and examples for its components, so that the API can be adopted and used efficiently and effectively.
* **Inclusive language** helps ensure that our terminology is free of offensive or exclusionary language.
* **Security** is extremely important for any API. Over 90% of organizations that use APIs have one or more security incidents per year.

You can also generate API changelogs to help your API consumers and developers understand how your API changes from version to version. This allows you to assess backwards compatibility and breaking changes before they reach production.

## Why Validate and Score OpenAPI Specification Files?

As services proliferate in an organization, teams need a common place to store their versioned API spec files. The API Insights service stores multiple versions of both released and release-candidate API specification files, and generates difference (diff) reports across multiple versions and revisions of your spec files.

Teams also need to work collaboratively on spec files in GitHub or other version control systems. The API Insights CLI allows you to integrate the spec file analyzers into a CICD or local commit pipeline. 

When working across multiple teams, developers can end up with inconsistent API specifications. Inconsistencies make it difficult for API consumers to integrate services across multiple APIs. API Insights allows you to validate and score an API spec file against specific API guidelines. 

In addition, if API changes are not backwards compatible with previous versions, your organization can lose the trust of your developers and consumers. API Insights can identify and report changes that are not backwards compatible.

Another common issue which developers encounter is a lack of consistent documentation of API changes across releases. With API Insights, you can assess the completeness of any documentation generated from an OpenAPI spec file.

## What Works With API Insights?

API Insights leverages [APIClarity](https://apiclarity.io) to analyze API drift. This allows API Insights to identify Zombie and Shadow APIs on currently running services. A Zombie API is an API that has been deprecated and should no longer be running on the service. A Shadow API is an API path that is not documented, but is still working on a service. Either of these can pose security and backwards compatibility risks.

## How Does API Insights Work?

The overall solution flow of API Insights is as follows:

![Solution flow diagram for API Insights](/images/solutionFlow.svg)

API Insights stores its analysis information remotely and presents its data through a browser-based dashboard. From the API Insights dashboard, you can view analysis scores and reports, download specific versions of spec files, see diff reports, and more. You can analyze a spec file by committing it to a GitHub repository that has been configured to run API Insights in its CI/CD pipeline, by uploading it to the API Insights dashboard UI, or by using the local CLI.

Although the API Insights workflow contains multiple entry points, the overall flow looks something like the following:

1. Author your API spec file locally.

1. **To analyze and iterate on your API spec file locally**, use either the [API Insights extension](../guides/vscode-extension.md) for Visual Studio Code or the [API Insights local CLI](../references/clidocs/apiregistryctl.md) to run the API Insights analyzers and view the output report. You can then modify your file and re-run the analyzers to improve your scores. Note that using this method does not upload your spec file or analysis data to the API Insights service for others to view. For more information, see [API Insights CLI (api-insights-cli) Overview](/references/clidocs/cli-getting-started.md) and [Using the API Insights Extension for Visual Studio Code](/guides/vscode-extension.md)
1. **To upload your spec file to the API Insights service**, trigger the analyzers, and present the resulting analysis data in the API Insights dashboard UI, do one of the following:
   1. Upload your spec file directly in the API Insights dashboard UI.
   1. Commit your spec file to a GitHub repository that has been configured to run [API Insights in a CI/CD pipeline](../guides/cicd-setup-guide.md). For more information, see [Setting Up API Insights in a CI/CD Pipeline](/guides/cicd-setup-guide.md)
   1. Use either the Visual Studio Code extension or the local CLI to upload your spec file to the remote service and trigger the analyzers.
1. If you uploaded your spec file to the remote service, check the dashboard to view your spec file's scores, reports, diff comparisons, and more. The dashboard tracks multiple API spec files and versions of those spec files, so you can quickly view reports and analyses for several products or services. Here you can see detailed line-by-line analysis of your spec files, including severity ratings and remediation recommendations.
1. Download the spec file from the dashboard UI or by cloning it from the GitHub repository to your local environment.
1. Use the analyzer data to iterate on the spec file to improve its scores.
