# Getting Started with an API Insights Service

To get started with API Insights, install its service, which allows you and others to upload and analyze OpenAPI spec files and view their analysis data remotely.

## Prerequisites

* Install and configure the following tools:
  * [kubernetes](https://kubernetes.io/)
  * [kuebctl](https://kubernetes.io/docs/reference/kubectl/)
  * [helm](https://helm.sh/).
* Install an application for managing a local Kubernetes cluster and associated tools. For example, [Rancher Desktop](https://rancherdesktop.io/) allows you to locally set up Kubernetes, `kubectl` and `helm`. Other Kubernetes setup applications include *Minikube* and *Kind*.

## Setting Up the API Insights Service

1. Run the following to add the API Insights repository to your Helm client:
   ```shell
   helm repo add api-insights https://ciscodevnet.github.io/api-insights-helm-charts/
   ```

1. Run the following to deploy the API Insights dashboard UI and remote service in the `api-insights` namespace with Helm:
   ```shell
   helm install api-insights api-insights/api-insights -n api-insights --create-namespace
   ```

1. Run the following to set Kubernetes to wait until API Insights is ready and running:
   ```shell
   kubectl wait --for=condition=ready pods --all --timeout=300s -n api-insights
   ```

> **NOTE:** Because the API Insights service code is being migrated to public GitHub and the Helm charts may not be updated to work with the latest version, you may receive a timeout error.

1. Run the following to expose the API Insights UI and service ports:
   ```shell
   kubectl -n api-insights port-forward svc/api-insights 8080:8080
   ```

1. Check the API Insights dashboard UI in your local browser by visiting [http://localhost:8080/](http://localhost:8080/).

    ![API Insights UI](/images/get-started/api-insights-ui.png)

1. Clone the API Insights GitHub repository:
    ```
    git clone https://github.com/cisco-developer/api-insights.git
    ```
1. Create a service in the dashboard UI. The following screenshots show the creation of a service called `catalogue`:

    ![create service](/images/get-started/add-service.png)
    ![service created](/images/get-started/service-added.png)

## Uploading API Spec Files and Creating A Diff Report

1. Click the **Upload New Spec** button to upload a spec file to the service. The following example uses the file `samples/init-spec/v0.0-rev2/catalogue.json`.
    ![upload v0.0-rev2](/images/get-started/upload-spec-v0.0-rev2.png)

1. In the dashboard UI, click the **timeline** dropdown, then select a version of the spec file. API Insights displays the results of the analysis. If the UI does not display the analysis results, you may need to wait for a short itme or refresh the page in your browser.
    ![v0.0-rev2 result](/images/get-started/v0.0-rev2-result.png)

1. Upload another spec file to the service. The following example uses the file `samples/init-spec/v0.1-rev1/catalogue.json`. The analysis results for this file should report some rules violations.
    ![v0.1-rev1 result](/images/get-started/v0.1-rev1-result.png)

1. Navigate to the **Comparison** page and select the two versions that you uploaded in the previous steps. The dashboard will generate a report showing the differences between the two, and any incompatibilities between the versions.
    ![compare spec](/images/get-started/compare-spec.png)
    ![compare result](/images/get-started/compare-result.png)

### Uninstalling the Service
To uninstall the API Insights service and dashboard, run the following:

   ```shell
   kubectl delete ns api-insights
   helm repo remove api-insights  
   ```
