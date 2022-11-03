# Using the API Insights Extension for Visual Studio Code

API Insights is available as an extension for Visual Studio Code. The extension lets you analyze local spec files, view spec file information from the remote API Insights service, download remote spec files, or compare remote spec files to local spec files.

## Prerequisites
* Install Visual Studio Code from [https://code.visualstudio.com/Download](https://code.visualstudio.com/Download).

## Installation and Configuration

### Installing the API Insights Extension

1. Choose one of these two methods to find API Insights Extension:
    Method 1:
    1. In Visual Studio Code, click the **Extensions** button.
       ![The Extensions button in Visual Studio Code.](/images/extension-button.PNG)
    2. On the Extensions panel, enter "api insights" in the search field and press **Enter**.
       ![Search result page in VSCode](/images/extension-api-insights-in-srp.png)
    3. In the search results, select _API Insights_.

    Method 2:
    1. Navigate to the extension on the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=CiscoDeveloper.api-insights) in your browser.
    2. Click the **Install** button to install the extension.
    3. Click **Open Visual Studio Code**

2. Click the **Install** button on the extension's Details page.

When the installation is complete, the extension will appear in the list of extensions as shown below, and the API Insights icon will appear in the left sidebar.

![Click on the API Insights entry in the list of extensions to open the extension UI.](/images/extension-list.PNG)

Click on the API Insights icon on the left sidebar, shown below, to open the extension.

![The API Insights icon in the left sidebar.](/images/extension-icon.PNG)

### Configuring the API Insights Extension

To open the settings for the API Insights extension, click on its icon in the left sidebar to open the extension, then click on the gear icon to open its settings.

![Click on the gear icon in the upper-left of the extension UI to open the extension settings.](/images/extension-settings-icon.png)

## Using API Insights in Visual Studio Code

### Analyzing a Local Spec File

To run the API Insights analyzers on a local JSON or YAML file, open the file while the extension is active and properly configured. The extension will automatically analyze and lint the spec file.

The spec file's overall score appears in the status bar at the bottom of the screen.

![After you open a spec file, API Insights automatically analyzes it and displays the spec file's overall score in the status bar.](/images/extension-score.png)

If API Insights finds any issues with the spec file, those issues appear in the **Problems** tab of the integrated Visual Studio Code console.

![](/images/extension-problems.png)

Click on any entry in the console output to go to the line where that issue was found. The extension also highlights issues line-by-line in the file itself, and you can hover over the highlighted portion to view the rule that was violated.

![](/images/extension-problems-output.png)

The Problems console appends the results of any analysis to the end of its output as a collapsible entry, allowing you to open and analyze multiple files. When you click on a problem in the output, Visual Studio Code takes you to the line where that issue was detected in that particular file. To view only the analysis results of the currently active file tab, click on the **funnel** icon in the **Filter** field of the Problems console, then select **Show Active File Only** as shown here:

![](/images/extension-output-filter.png)

After you make changes to your spec file, save it to trigger the API Insights analyzers again.

### Using the Extension to View API Scores from the Remote Service

You can also use the API Insights extension for Visual Studio Code to view the analysis information for APIs that are hosted in the API Insights remote service.

1. Click on the API Insights icon on the left sidebar to open or close the API Insights service pane, which lists all of the organizations on the remote service.
   ![](/images/extension-ui-collapsed.png)
1. Click on any organization in the service pane to open or close its list of APIs.
   ![](/images/extension-ui-expanded.png)
1. Click on an API to view the details for that API. From this point on, the UI and features that you see in Visual Studio Code are the same as those on the browser-based API Insights dashboard.
1. To view details for a particular version of the spec file, scroll down to the **Version History** section and click on a version to expand its information.
  1. To view the full analysis report for that version of the spec file, click on the **View Full Report** icon in the lower right.
  1. Hover over the **ellipsis icon** to download the spec file or compare it to a local spec file.
  1. To view the issues that API Insights detected in that spec file, click on the **Open in Editor** icon in the lower right of the information tile, as shown here:
    ![](/images/extension-ui-open.png)
    See the next section for more information about how to use this feature.

  > **Note:** Currently, the **Download** feature does not work.

### Modifying a Spec File from the Remote Service

When you click on **Open in Editor**, the spec file does not directly open in the Visual Studio Code editor. Instead, the issues that API Insights detected in that spec file open in the **Problems** console. However, if you click on an issue from a remote API spec file in the **Problems** console, Visual Studio Code returns an error.

To modify a remote spec file, do the following:

1. Clone the spec file from GitHub.
2. Open the cloned spec file locally in Visual Studio Code to run the API Insights extension on it.
3. Modify the local spec file, to resolve the issues that the extension detected. Each time you save the file, the extension will re-analyze it and display the new score and list of issues.
4. When you are finished modifying the file locally, commit it to GitHub to upload it to the remote service as described in [Using API Insights in your CI/CD Pipeline](/guides/cicd-setup-guide.md).

### Uninstalling the Extension

To uninstall the API Insights extension, do one of the following:

* Open your extensions list and click on the API Insights extension to open its details, then click **Uninstall**.
* In the extensions list, click on the settings icon for API Insights, then click **Uninstall**.
