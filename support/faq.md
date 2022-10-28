## What is API Insights?
API Insights is an open-source tool that Cisco is developing to help developers improve API quality. 

The API Insights Extension for Visual Studio Code allows developers to leverage the functionalities of API Insights within the Integrated Development Environment.

## What is APIClarity?
APIClarity captures and analyzes API traffic to help you identify potential security risks. The tool is open source and uses a service mesh framework.

Visit the [APIClarity Official site](https://apiclarity.io) to get more details.

## Frequently Asked Questions (FAQ)

### Q: Do I need an OpenAPI spec file in order to use API Insights?

**A:** Yes, but the spec file can be in JSON or YAML format.

### Q: If I do not have an OpenAPI spec file for my service, can I still use API Insights?

**A:** Yes, you can set up API Clarity and use it to generate an OpenAPI spec file based on your API's traffic.

### Q: What prerequisites do I need to set up in order to use API Clarity?

**A:** API Clarity performs runtime traffic analysis, so you need to set up an agent to capture data from the service mesh (such as [Istio](https://istio.io/)) or API Gateway (such as [Kong](https://konghq.com/).

### Q: How do I analyze my OpenAPI Specification (OAS) file?

**A**: You can analyze an API spec file in three ways:

1. In the **API Insights Dashboard**: A quick and easy way is to upload your OAS file directly to the Dashboard with the **Upload a new Spec** button. See [Getting Started](/overview/getting-started.md) for detailed instructions.
1. Through the **API Insights Extension for Visual Studio Code**: API Insights is available as an extension for Visual Studio Code. The extension lets you analyze local spec files, view spec file information from the remote API Insights service, download remote spec files, and compare remote spec files to local spec files. For more information, see [Using the API Insights Extension for Visual Studio Code](/guides/vscode-extension.md).
1. Using the **API Insights CLI** to integrate API Insights into your **CI/CD pipeline**: A more scalable solution for analyzing your spec files is to integrate API Insights into your CI/CD pipeline using the API Insights CLI. Best practice for this integration is to create a new release for the updated OAS file in your GitHub repository, so that API Insights can analyze the OAS file, calculate its score, and compare it to a benchmark score in the CI/CD pipeline before the spec file is deployed. See "Setting up API Insights in a CI/CD pipeline" for more information.

### Q. What should I do if I have problems logging in?
**A**: The authentication and authorization vary depending on how your instances are connected to the service. Please make sure you have a working APIClarity service and correct settings for authentication, such as the `Endpoint URL`, `Token Type`, and `Token value` fields.

### Q. How does the "Spec format" setting work?
**A**: An API spec file may be represented either in JSON or YAML format. This setting allows you to choose the default format used for downloaded or copied API specs files.

### Q. How do you associate a spec file with a service?
**A**: Before you can click the **Open in editor** button in [API Detail View], you must have associated a local spec file with this service, otherwise the extension does not know what file it needs to open. 

The extension provides three different ways to create this association:
1. Upload a local spec file to API Clarity using the [Specs] tab to upload a local spec file to APIClarity.
2. Download a provided spec file from API Clarity, using the [Specs] tab to download an existing provided spec file. Another developer could have uploaded this provided spec file.
3. Download a reconstructed spec file from API Clarity, using [Specs] tab to download a reconstructed spec file if there is an existing version reconstructed by others, or you can reconstruct a new one from scratch.
