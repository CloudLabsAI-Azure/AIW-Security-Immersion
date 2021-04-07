# Module 7 – Exporting ASC information to a SIEM


## Overview

In this module, you will configure the continuous export for Log Analytics workspace, exporting security alerts, recommendations, secure score, and security findings. Moreover, you will learn how to enable the integration between Azure Security Center and Azure Sentinel.

### Exercise 1: Using continuous export

Azure Security Center generates detailed security alerts and recommendations. You can view them in the portal or through programmatic tools. You might also need to export some or all of this information for tracking with other monitoring tools in your environment.

Continuous export lets you fully customize what will be exported, and where it will go. Even though the feature is called continuous, there's also an option to export weekly snapshots of secure score or regulatory compliance data.

1.	Launch **Azure Portal** using the desktop icon on the **JumpVM** and login with the Azure credentials from the Lab **Environment Details** tab

2.	Type **Security Center** in the search box located on the top of the **Azure Portal** page and click on it. Next, click on **Pricing & settings** under the **Management** tab in the left sidebar.

3.	Select **Your Subscription**.

   ![Pricing & settings page](../Images/asc-pricing-settings-sub.gif?raw=true)

4.	From the Azure Defender plans sidebar, click on **Continuous export** under the **Settings** section.

5.	Here you can configure the streaming export setting of Security Center data to multiple export targets either Event Hub or Log Analytics workspace.

6.	Select the **Log Analytics workspace** option.

   ![continuous-export](../Images/continuous-export.png)

7.	Under the **Exported data types** section of the **Continuous export** page, select **Security recommendations, Secure score (Preview) and Security alerts** – as you can see, all recommendations, severities, controls, and alerts are selected.

8.	Under the **Export configuration** section of the **Continuous export** page, select the resource group: *asclab* from the drop down menu.

9.	Under the **Export target** section, select the target Log Analytics workspace: *asclab-la-{DeploymentID}*

   **Note**: Deployment ID can be obtained from the Lab Environment Details tab.

10. Click on the **Save** button on the top menu.

    ![Continuous export settings page](../Images/asc-continuous-export-settings.gif?raw=true)

> Note: Exporting Security Center's data also enables you to use experiences such as integration with 3rd-party SIEM and Azure Data Explorer.

11. Type **Log Analytics workspaces** in the search box located on the top of the **Azure Portal** page and click on it or [click here](https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.OperationalInsights%2Fworkspaces).

12. Click on the **asclab-la-{DeploymentID}** workspace.

13. From the workspace’s sidebar, click on the **Logs** button under the **General** section.

14. On the welcome page, click on the **Get Started** button and then close the **Queries** window.

    ![Continuous export settings page](../Images/log-analytic-started.png)

15. From the left pane select the **Tables** tab and **enable** the **Show tables with no data** option to see the following tables: `SecurityEvent`, `SecurityBaseline`, `SecurityBaselineSummary` and  `UpdateSummary` in `Security and Audit`.

   ![Tables page](../Images/showtables.png)

16. Query the tables to validate data streaming - For example, Click on **Tables** expand **Security and Audit** double click on **Security Event** to open in the query window. Now click on **Run** and see the results below.

   ![Respective tables in the Log Analytics workspace](../Images/Log-editor-tables.png)

### Exercise 2: Integration with Azure Sentinel

Integration with Azure Sentinel will enable centralized monitoring of alerts and discovery data. Integrating with Azure Sentinel allows you to better protect your cloud applications while maintaining your usual security workflow, automating security procedures, and correlating between cloud-based and on-premises events.

1. Type **Azure Sentinel** in the search box located on the top of the **Azure Portal** page and click on it or [click here](https://portal.azure.com/#blade/Microsoft_Azure_Security_Insights/WorkspaceSelectorBlade).

2.	On the **Azure Sentinel** blade, click on the **Create Azure Sentinel** button – for this exercise, we’ll use the same Log Analytics workspace used by Security Center.

   ![connect-workspace1](../Images/sentinel.png)

3.	On the **Add Azure Sentinel to a workspace**, select **asclab-la-{DeploymentID}** workspace. Click on **Add**.

   ![Add sentinel](../Images/sentineladd.png)

4.	Adding Azure Sentinel to workspace asclab-la-{DeploymentID} is now in progress. This process will take few minutes to complete. 

5.	Once the deployment of workspace is completed you will get a notification as **Successfully added Azure Sentinel**. **Refresh** the page to see the workspace listed on Azure Sentinel page.

  ![Add sentinel](../Images/sentinelws.png)

6. Select the workspace **asclab-la-{DeploymentID}** on the **Azure Sentinel** page. 

7. Next, select the **News and guides** option from the General section of the **Azure Sentinel** page. Once the **News and guides** open, use the Azure Security Center connector to enable the integration.

8.	From Azure Sentinel sidebar, click on the **Data connectors** under the **Configuration** section.

9.	On the **Data connectors** page, use the search field and type: *Azure Defender*.

10. Select the **Azure Defender** connector and then click on **Open connector page**.

    ![ASC pricing & settings page](../Images/Azure-defender-open.png)

11. On the Configuration section, locate **Your subscription** and change the toggle button to **Connected**.

    ![Connect Azure Security Center to Azure Sentinel](../Images/connected.png)

12. On the Create incidents (recommended) click on the **Enable** button to create incidents automatically from all alerts generated in this connected service.

    ![Enable incidents](../Images/asc-sentinel-enable-incidents.gif?raw=true)
 
 >You may have to scroll down to find the option.

### Summary

In this lab you have completed configuring continuous export for Log Analytics workspace, exporting security alerts, recommendations, secure score, and security findings and enable the integration between Azure Security Center and Azure Sentinel.

Now you can move on to the next module by clicking on the Next button at the bottom right of the screen.
