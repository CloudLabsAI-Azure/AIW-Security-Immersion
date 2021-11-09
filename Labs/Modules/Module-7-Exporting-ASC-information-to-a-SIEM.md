# Module 7 – Exporting ASC information to a SIEM


## Overview

In this module, you will configure the continuous export for Log Analytics workspace, exporting security alerts, recommendations, secure score, and security findings. Moreover, you will learn how to enable the integration between Azure Security Center and Azure Sentinel.

### Exercise 1: Using continuous export

Azure Security Center generates detailed security alerts and recommendations. You can view them in the portal or through programmatic tools. You might also need to export some or all of this information for tracking with other monitoring tools in your environment.

Continuous export lets you fully customize what will be exported, and where it will go. Even though the feature is called continuous, there's also an option to export weekly snapshots of secure score or regulatory compliance data.

1.  Type **Security Center** in the search box located on the top of the **Azure Portal** page and click on it.

     ![](https://github.com/Divyasri199/AIW-Security-Immersion/blob/main/Labs/Images/security%20center.png?raw=true)
     
1. Under **Microsoft Defender for Cloud** page, click on **Getting started (1)**, and navigate to **Install agents (2)** then select **Pricing & settings page (3)**.

    ![](../Images/pricingandsetting.png)
    
1. Select **Your Subscription** under the Environment settings.

   ![](../Images/envset.png)


3.	Under **Settings** section, click on **Continuous export**.

    ![](../Images/continuousexport.png)

4.	Here you can configure the streaming export setting of Security Center data to multiple export targets either Event Hub or Log Analytics workspace.

5.	Select the **Log Analytics workspace (1)** option and follow the below steps:

    - Exported data types:

        - Check the box next to  **Security recommendations (2)**

        - Check the box next to **Secure score (3)**

        - Check the box next to **Security alerts (4)**

     ![continuous-export](../Images/LAW1.png)
     
     - Export frequency:

        - Check the box next to **Streaming updates (5)** and **Snapshots (Preview) (6)**

     - Export configuration:

          - Resource group: Select **asclab (7)** from drop-down list

     - Export target:

          - Subscription : Select your **Subscription (8)**

          - Select target workspace: Select **asclab-la-{DeploymentID} (9)**

     -  Click on **Save (10)**

        ![](../Images/LAW2.png)

     > **Note:** Exporting Security Center's data also enables you to use experiences such as integration with 3rd-party SIEM and Azure Data Explorer.

10. Search for **Log Analytics workspaces** in the search box located on the top of the **Azure Portal** page and click on it or [click here](https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.OperationalInsights%2Fworkspaces).

11. Click on the **asclab-la-{DeploymentID} (1)** workspace and select **Logs(2)** button under the **General** section.

     ![](../Images/LAW3.png) 

13. On the welcome page, close the **Queries** window.

   ![Continuous export settings page](../Images/log-analytic-started2.png)

14. From the left pane select the **Tables** tab and **enable** the **Show tables with no data** option to see the following tables: `SecurityEvent`, `SecurityBaseline`, `SecurityBaselineSummary` and  `UpdateSummary` in `Security and Audit`.

   ![Tables page](../Images/showtables.png)

15. Query the tables to validate data streaming - For example, Click on **Tables (1)** expand **Security and Audit (2)** double click on **Security Event (3)** to open in the query window. Now click on **Run (4)** and see the results below.

   ![Respective tables in the Log Analytics workspace](../Images/Log-editor-tables.png)
> **Note:** Since the continuous export was just enabled, you may need to wait for sometime for new events to show up.

### Exercise 2: Integration with Azure Sentinel

Integration with Azure Sentinel will enable centralized monitoring of alerts and discovery data. Integrating with Azure Sentinel allows you to better protect your cloud applications while maintaining your usual security workflow, automating security procedures, and correlating between cloud-based and on-premises events.

1. Search for **Azure Sentinel** in the search box located on the top of the **Azure Portal** page and click on it or [click here](https://portal.azure.com/#blade/Microsoft_Azure_Security_Insights/WorkspaceSelectorBlade).

    ![](../Images/Azuresenitel.png)

2.	On the **Azure Sentinel** blade, click on the **Create Azure Sentinel** button – for this exercise, we’ll use the same Log Analytics workspace used by Security Center.

   ![connect-workspace1](../Images/sentinel.png)

3.	On the **Add Azure Sentinel to a workspace**, select **asclab-la-{DeploymentID}** workspace. Click on **Add**.

   ![Add sentinel](../Images/sentineladd.png)

4.	Adding Azure Sentinel to workspace asclab-la-{DeploymentID} is now in progress. This process will take few minutes to complete. 

5.	Once the deployment of workspace is completed you will get a notification **Successfully added Azure Sentinel**. Refresh the web browser page to see the workspace listed on Azure Sentinel page.

  ![Add sentinel](../Images/sentinelws.png)

6. Select the workspace **asclab-la-{DeploymentID}** on the **Azure Sentinel** page. 

7. From Azure Sentinel side pane, click on the **Data connectors** under the **Configuration** section.

   ![](../Images/dataconnectors.png)
    

8.	On the **Data connectors** page, use the search field and type: *Microsoft Defender*. Select the **Microsoft Defender for Cloud** connector and then click on **Open connector page **.

   ![ASC pricing & settings page](../Images/defender.png)

10. On the Configuration section, locate **Your subscription** and change the toggle button to **Connected**.

    ![Connect Azure Security Center to Azure Sentinel](../Images/connected.png)

11. On the Create incidents (recommended) click on the **Enable** button to create incidents automatically from all alerts generated in this connected service.

    ![Enable incidents](../Images/asc-sentinel-enable-incidents.png)
 
 > **Note:** You may have to scroll down to find the option.

### Summary

In this lab you have completed configuring continuous export for Log Analytics workspace, exporting security alerts, recommendations, secure score, and security findings and enable the integration between Azure Security Center and Azure Sentinel.

Now you can move on to the next module by clicking on the Next button at the bottom right of the screen.
