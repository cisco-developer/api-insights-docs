# Frequently Asked Questions (FAQ)

## General Questions

### Q: What is API Insights?

**A:** API Insights is an open-source tool that Cisco is developing to help developers improve API quality.  The API Insights Extension for Visual Studio Code allows developers to leverage the functionalities of API Insights within the Integrated Development Environment.

### Q: I already use open-source tools like Spectral and OpenAPI-diff. How does API Insights help me?

**A:** API Insights provides lifecycle management of your APIs, and allows developers, DevOps, DevSecOps and compliance teams to collaborate to improve API quality. It provides static, rules-based analysis of API spec files, and allows teams to collaboratively use that information to iterate on APIs. 

### Q: What is APIClarity?

**A:** APIClarity captures and analyzes API traffic to help you identify potential security risks. The tool is open source and uses a service mesh framework.

Visit the [APIClarity Official site](https://apiclarity.io) to get more details.

## Operational Questions

### Q: How do I analyze my OpenAPI Specification (OAS) file?

**A:** You can analyze an API spec file in three ways:

1. In the **API Insights Dashboard**: A quick and easy way is to upload your OAS file directly to the Dashboard with the **Upload a new Spec** button. See [Getting Started](/overview/getting-started.md) for detailed instructions.
1. Through the **API Insights Extension for Visual Studio Code**: API Insights is available as an extension for Visual Studio Code. The extension lets you analyze local spec files, view spec file information from the remote API Insights service, download remote spec files, and compare remote spec files to local spec files. For more information, see [Using the API Insights Extension for Visual Studio Code](/guides/vscode-extension.md).
1. Using the **API Insights CLI** to integrate API Insights into your **CI/CD pipeline**: A more scalable solution for analyzing your spec files is to integrate API Insights into your CI/CD pipeline using the API Insights CLI. Best practice for this integration is to create a new release for the updated OAS file in your GitHub repository, so that API Insights can analyze the OAS file, calculate its score, and compare it to a benchmark score in the CI/CD pipeline before the spec file is deployed. See "Setting up API Insights in a CI/CD pipeline" for more information.

### Q: How can I integrate API Insights into my CI/CD pipeline?

**A:** To integrate API Insights into your GitHub CI/CD pipeline, see [Set Up API Insights in a CI/CD Pipeline](/guides/cicd-setup-guide.md).

### Q: Can I use API Insights in a different CI/CD platform?

**A:** Yes. As long as the platform can accommodate the API Insights CI/CD process documented in [Set Up API Insights in a CI/CD Pipeline](/guides/cicd-setup-guide.md). Using the platform, you must be able to:

* Execute API Insights CLI commands in the platform. The API Insights CLI is required to actually call the API Insights service to run analyzers and upload the results and the spec file to the API Insights Dashboard. For more information about the API Insights CLI, see the [API Insights CLI (api-insights-cli) Overview](/references/clidocs/cli-getting-started.md) and associated CLI documentation.
* Use a `.yaml` configuration file to control the CI/CD pipeline. You may need to adapt the example `api-insights.yaml` file to your platform and environment.
* Create a unique tag and assign it to a specific update or commit in the repository. API Insights needs to be able to detect when a new spec file is uploaded, or an existing one is updated.
* Execute API Insights CLI commands in response to the events described above.

### Q: How do I associate a spec file with a service?
**A:** To associate a spec file with a service, upload the spec file to the service. You can upload a spec file in several ways:

1. Upload the spec file directly in the API Insights dashboard UI.
1. Commit a new version of the file to a GitHub repository that has been configured to run API Insights as part of its CI/CD pipeline.
1. Use the API Insights local CLI to upload the spec file.
1. Use the API Insights extension for Visual Studio Code.
