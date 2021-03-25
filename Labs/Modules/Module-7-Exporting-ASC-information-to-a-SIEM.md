# Module 7 – Exporting ASC information to a SIEM


## Overview

In this module, you will understand how to configure the continuous export for Log Analytics workspace, exporting security alerts, recommendations, secure score, and security findings. Moreover, you will learn how to enable the integration between Azure Security Center and Azure Sentinel.

### Exercise 1: Using continuous export

1.	Click on the Azure Portal icon on the JumpVM and login with the Azure credentials from the Lab Environment output page.

2.	On Security Center’s sidebar, click on **Pricing & settings**.

3.	Select **Your Subscription**.

![Pricing & settings page](../Images/asc-pricing-settings-sub.gif?raw=true)

4.	From the Azure Defender plans’ sidebar, click on **Continuous export**.

5.	Here you can configure streaming export setting of Security Center data to multiple export targets either Event Hub or Log Analytics workspace.

6.	Select the **Log Analytics workspace** option.

7.	On the Exported data types, select **Security recommendations, Secure score (Preview) and Security alerts** – as you can see, all recommendations, severities, controls, and alerts are selected.

8.	On the Export configuration, select a resource group: *asclabs*

9.	On the Export target, select the target Log Analytics workspace: *asclab-la-{DeploymentID}*

    **Note**: Deployment ID can be obtained from the Lab Environment Details tab.

10.	Click on the **Save** button on the top menu.

![Continuous export settings page](../Images/asc-continuous-export-settings.gif?raw=true)

> Note: Exporting Security Center's data also enables you to use experiences such as integration with 3rd-party SIEM and Azure Data Explorer.

11.	On the Azure portal, navigate to **Log Analytics workspaces** service or [click here](https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.OperationalInsights%2Fworkspaces).

12.	Click on the **asclab-la-{DeploymentID}** workspace.

13.	From the workspace’s sidebar, click on the **Logs** button.

14.	On the welcome page, click on the **Get Started** button and then **close the Queries window**.

![Continuous export settings page](../Images/log-analytic-started.png)

15.	From the left pane, notice the following tables: `SecureityEvent`, `SecurityBaseline`, `SecurityBaselineSummary` and  `UpdateSummary` in **Security and Audit**.

![Respective tables in the Log Analytics workspace](../Images/Log-editor-tables.png)

16.	Query the tables later on to validate data streaming - double click on the desired table to open a new query. Then click **Run**.

![Respective tables in the Log Analytics workspace](../Images/log-editor-run.png)

### Exercise 2: Integration with Azure Sentinel

1.	On the Azure portal, navigate to **Azure Sentinel** service or [click here](https://portal.azure.com/#blade/Microsoft_Azure_Security_Insights/WorkspaceSelectorBlade).

2.	On the Azure Sentinel workspaces, click on **Connect** workspace button – for this exercise we’ll use the same Log Analytics workspace used by Security Center.

3.	On the **Add Azure Sentinel** to a workspace, select **asclab-la-{DeploymentID}** workspace. Click **Add**.

4.	Adding Azure Sentinel to workspace asclab-la-{DeploymentID} is now in progress. This process will take few minutes. 

5.	Once Sentinel News and guides opens, use the Azure Security Center connector to enable the integration.

6.	From Sentinel’s sidebar, click on the **Data connectors**.

7.	On the Data connectors page, use the search field and type: *Azure Defender*.

8.	Select the **Azure Defender** connector and then click on **Open connector page**.

![ASC pricing & settings page](../Images/Azure-defender-open.png)

9.	On the Configuration section, locate the **Your subscription** and change the toggle button to **Connect**. Wait for the connection status to be: `Connected`.

![Connect Azure Security Center to Azure Sentinel](../Images/asc-sentinel-data-connector-page.png)

10.	On the Create incidents (recommended) click on the **Enable** button to create incidents automatically from all alerts generated in this connected service.

![Enable incidents](../Images/asc-sentinel-enable-incidents.gif?raw=true)

### Summary

In this lab you have completed configuring continuous export for Log Analytics workspace, exporting security alerts, recommendations, secure score, and security findings and enable the integration between Azure Security Center and Azure Sentinel.

Now you can move on to the next module by clicking on the Next button at the bottom right of the screen.
