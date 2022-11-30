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

API Insights leverages [APIClarity](https://apiclarity.io) to analyze API drift. This allows API Insights to identify Zombie and Shadow APIs on currently-running services. A Zombie API is an API that has been deprecated and should no longer be running on the service. A Shadow API is an API path that is not documented, but is still working on a service. Either of these can pose security and backwards compatibility risks.

## How Does API Insights Work?

API Insights stores its analysis information and reports remotely and presents its data through a browser-based dashboard. From the API Insights dashboard, you can view analysis scores and reports, download specific versions of spec files, see diff reports, and more. You can analyze a spec file by committing it to a GitHub repository that has been configured to run API Insights in its CI/CD pipeline, through the API Insights dashboard UI, or through the **local CLI**.

The overall solution flow of API Insights is as follows:

![Solution flow diagram for API Insights](/images/solutionFlow.svg)

API Insights stores its analysis information remotely and presents its data through a browser-based dashboard. From the API Insights dashboard, you can view analysis scores and reports, download specific versions of spec files, see diff reports, and more. You can analyze a spec file by committing it to a GitHub repository that has been configured to run API Insights in its CI/CD pipeline, by uploading it to the API Insights dashboard UI, or by using the local CLI.

Although the API Insights workflow contains multiple entry points, the overall flow looks something like the following:

1. Author your API spec file locally.
1. Use either the [API Insights extension](../guides/vscode-extension.md) for Visual Studio Code or the [API Insights local CLI](../references/clidocs/api-insights-cli.md) to analyze your spec file. Both of these options allow you to analyze a local spec file and view analysis information from the API Insights remote service. Iterate on your local spec file to raise its scores before you commit it to your repository.
1. Commit your spec file to a GitHub repository that has been configured to run [API Insights in a CI/CD pipeline](../guides/cicd-setup-guide.md). Create a GitHub release tag to trigger the API Insights analyzers and differentiate the new version of the spec file from previous versions. API Insights runs its analyzers on your spec file as GitHub actions, and passes the results into the API Insights dashboard. You can also analyze a spec file in the following ways:
   1. Upload your spec file directly to the API Insights dashboard UI.
   1. Run the local API Insights CLI to analyze the spec file in your local environment.
   1. Use the API Insights Extension for Visual Studio Code to run the API Insights analyzers in your local IDE.
1. If you uploaded your spec file to the API Insights remote service, check the **API Insights dashboard** to view your recently submitted spec file's scores, reports, diff comparisons, and more. The dashboard tracks multiple API spec files and versions of those spec files, so you can quickly view reports and analyses for several products or services. Here you can see detailed line-by-line analysis of your spec files, including severity ratings and remediation recommendations. 
1. Iterate on your published spec file by cloning the spec file from the GitHub repository to your local environment and repeating steps 2 and 3 to raise your API's scores.

## How Can I Get Started With API Insights?

To get started with API Insights, see [Getting Started with an API Insights Service](/overview/getting-started.md).

**Prerequisites** for getting started with API Insights are given in the Getting Started with an API Insights Service article, but are reproduced here for convenience. To get started with API Insights, you will need the following:
* An API spec file that conforms to the OpenAPI specification, in either `.json` or `.yaml` format. If you do not have an OpenAPI spec file, you can use [APIClarity](https://github.com/openclarity/apiclarity) to generate one based on your API's traffic.
* Install [Kubernetes](https://kubernetes.io/).
* Install [kuebctl](https://kubernetes.io/docs/reference/kubectl/).
* Install [helm](https://helm.sh/).
* Install an application for managing a local Kubernetes cluster and associated tools. For example, [Rancher Desktop](https://rancherdesktop.io/) allows you to locally set up Kubernetes, `kubectl` and `helm`. Other Kubernetes setup applications include *Minikube* and *Kind*.
* Install an agent to capture data from the service mesh (such as [Istio](https://istio.io/)) or API Gateway (such as [Kong](https://konghq.com/). [APIClarity](https://github.com/openclarity/apiclarity), a key component of API Insights which performs run time traffic analysis, requires a monitoring agent.
