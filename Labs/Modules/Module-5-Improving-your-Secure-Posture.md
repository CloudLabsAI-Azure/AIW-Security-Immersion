# Module 5 - Improving your Secure Posture

## Overview

This module will walk you through the process of using the vulnerability assessment for Virtual Machines and Containers, along with the usage of Workflow Automation and data query.

## Objectives

- Exercise 1: Vulnerability Assessment for Containers
- Exercise 2: Automate recommendations with workflow automation
- Exercise 3: Accessing your secure score via ARG

### Exercise 1: Vulnerability Assessment for Containers

Microsoft Defender for Cloud scans images in your Azure Container Registry (ACR) that are pushed and imported into the registry, it also contains any other images pulled within the last 30 days. Then, it exposes detailed findings per image. All vulnerabilities can be found in the following recommendations: **Vulnerabilities in Azure Container Registry images should be remediated (powered by Qualys).**

In this exercise, you will work on vulnerablity assessment for containers by uploading a image to your conatiner registry.

To simulate a container registry image with vulnerabilities, we will use ACR task commands and a sample image:

1. Search for **Container registries** in the search box located on the top of the **Azure Portal** page and click on it, or click [here](https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.ContainerRegistry%2Fregistries).

2. Copy the name or your container registry, for example: *asclabcrktfvrxcne4kki*

    ![acr-select](../Images/m5ex2step2.png)

3. In the Azure portal, open the **Cloud Shell** pane by selecting the toolbar icon directly to the right of the search textbox or clicking on [Azure Cloud Shell](https://shell.azure.com/).

    ![cloudshell-select](../Images/ex4-cloudshell.png)

4. If prompted to select either Bash or PowerShell, select **Bash**.

    ![cloudshell-select](../Images/bash.png)

5. When prompted, click **Create storage** and wait for the Azure Cloud Shell to initialize. 

6. Build a Linux container image from the hello-world image hosted at Microsoft Container Registry and push it to the existing Azure Container Registry instance on your subscription:
 
   Run the following two script blocks:

    ```
    echo FROM mcr.microsoft.com/azuredocs/aci-helloworld > Dockerfile
    ```

   Modify the following script to include your container registry name in the placeholder <your container registry name>

    ```
    az acr build --image sample/hello-world:v1 --registry <your container registry name> --file Dockerfile .
    ```

    ![Build Linux container in Cloud Shell](../Images/asc-build-linux-container-cloud-shell.gif?raw=true)

7. Wait for a successful execution message to appear. For example: Run ID: cf1 was successful after 10s.

8. The scan completes typically within a few minutes, but it might take up to 15 minutes for the vulnerabilities/security findings to appear on the Recommendations page.

9. Search for **Microsoft Defender for Cloud** in the search box located on the top of the **Azure Portal** page and click on it.

10. Click on **Recommendations (1)** from the left side pane under the **General** section. Under All recommendations, search and select **Azure registry container images should have vulnerabilities resolved(2)**.
 
     ![asd](../Images/lab5-14.png)

    > **Note**: If you don't see the above recommendation that means it is not loaded yet, and it could take up to 24 hours for all the recommendations to show up. It is possible that during lab time, this may not show up – which is the case sometimes. You can note down this step number, then continue to the next exercise and verify this later.

11. On the recommendation page, notice the following details in the upper section:

    - Unhealthy registries: **1/1**
    - Severity: **High**
    - Total vulnerabilities: **expect to see more than 2 vulnerabilities**

        ![](../Images/lab5-13.png)

12. Expand the **Affected resources (1)** section and notice the **Unhealthy registries** count which shows **1 container registry (2)** (asclab**xxx** here xxx is unique ID).

     ![](../Images/lab5-15.png)

13. On the **Security Checks** section, notice the number of vulnerabilities.

14. Click on the first security check to open the **XXXXXX- User(s) with Blank Password** pane.

    >XXXXXX is the ID of the security finding.

     ![](../Images/secure-M5-Ex2-S13.png)

   Notice the vulnerability description, general information (containing the Cvss 2.0 base score, etc.), remediation steps/workaround, additional information, and the affected (vulnerable) image. **Close this window.**

### Exercise 2: Automate recommendations with workflow automation

Every security program includes multiple workflows for incident response. The process might include notifying relevant stakeholders, launching a change management process, and applying specific remediation steps. With the help of workflow automation, you can trigger logic apps to automate processes in real-time with Microsoft Defender for Cloud events (security alerts or recommendations). 

In this Exercise, you will create a new Logic App and then trigger it automatically using the workflow automation feature when there is a change with a specific recommendation.

**Create a new Logic App:**

1. Search for **Logic Apps** in the search box located on the top of the **Azure Portal** page and click on it, or [click here](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Logic%2Fworkflows).

    ![](../Images/M5-ex3-1.png)
    
1. Click on **+ Add** to create a new Logic App.
    
    ![](../Images/M5-ex3-2.png)

1. On the **Create logic app** page, select **Consumption** plan and click on **select**.

    ![](../Images/newimg5.png)

1. On the Basics tab, enter the following details:
     
     - Subscription: Select your **Subscription** 
      
     - Resource group:  **asclab** 
 
     - Logic app name: Enter **Send-RecommendationsChanges<inject key="DeploymentID" enableCopy="false"/>**.

     - Location: Select the location of your **Resource group**
        
     - Enable log analytics: Select **No**

     - Select **Review + create** and then click on **Create**.

        ![](../Images/newimg6.png)

1. When the **Deployment** is completed click on **Go to resource**

    ![](../Images/gotoresource.png)

 then click on "Enable Legacy Designer." Once the "Legacy designer" popup appears, proceed by clicking on it.
 
1. Select **Logic app designer** from the left panel then click on **Enable Legacy Designer**. Once the **Legacy designer** popup appears, proceed by clicking on it. Scroll down and choose **Blank Logic App**. 

   ![](../Images/open-logic-app.png)

1. Search for **Security Center** in the search box and select **When a Microsoft Defender for Cloud Recommendation is created or triggered** from the list of **Triggers**

    ![](../Images/lab5-1.png)

1. Click on the **+ New step** button and type **Outlook send**.

    ![](../Images/newstep1.png)

1. From the list of actions, select the **Send an email (V2)** action to add it to the Designer.
     
    ![](../Images/emailv2.png)

   > **Note:** You will need to sign into your Outlook.com (Use Odl user from Environment details) and grant permissions for the Logic App to send email using your account.

1. In the Send an email (V2), select **Sign in**. Select the email address to sign in and enter the below email address in the **To** field.
   
      * Email/Username: <inject key="AzureAdUserEmail"></inject> 

    > Later, you will use the same email address to check if you have received an email using the workflow automation feature.

1. Click in the **Subject box**, then type: **Recommendation changed:**

1. Click just after Recommendation changed: to get your cursor in the right place. In the dynamic content box, click on the **Dynamic content** tab and then search and select `Properties Display Name` in the list (click Add dynamic content if it doesn’t pop out automatically).

1. Click into the Body text box and type the following:

    - **The following recommendation has been changed**</br>
    - **Recommendation:**</br>
    - **Description:**</br>
    - **Status:**</br>
    - **Link to recommendation:**</br>

1. Click just after each section, to get your cursor in the right place. In the **dynamic content box**, match each line to the following content by searching and selecting in the list:

   - Recommendation: `Properties Display Name`</br>
   - Description: `Properties Metadata Description`</br>
   - Status: `Properties Status Code`</br>
   - Link to recommendation: `Properties Links Azure Portal Uri`</br>

1. Verify that Your Logic App looks like the below screenshot and then click on **Save** in the Logic App Designer.

    ![Logic App worklfow](../Images/c10.png)

**Create a new workflow automation instance**

1. Search for **Microsoft Defender for Cloud** in the search box at the top of the **Azure Portal** page and click on it.

2. Select **Workflow automation (1)** under **Management** section from the left side pane, and click on **+ Add workflow automation (2)**.

    ![](../Images/workflow1.png)

3. A pane appears on the right side. Enter the following for each field:
    
   - General:
   
     * Name: **Send-RecommendationsChanges**
     * Description: **Send email message when a recommendation is created or triggered**
     * Subscription: **Your Subscription**
     * Resource group: **asclab**

        ![](../Images/lab5-2.png)
      
   - Trigger conditions:
   
     * Select Defender for Cloud data types: **Recommendation**
     * Recommendations name: **All recommendations selected**
     * Recommendation severity: **All severities selected**
     * Recommendation state: **All states selected**

        ![](../Images/lab5-3.png)
    
   - Actions:
   
     * Show Logic App instances from the following subscriptions: **Your Subscription**

     * Logic App name: **Send-RecommendationsChanges<inject key="DeploymentID" enableCopy="false"/>**
     
   Click **Create** to complete the task.

     ![](../Images/lab5-4.png)

4. Wait for the message **"Workflow automation created successfully. Changes may take up to 5 minutes to be reflected"** to appear. From now on, you will get email notifications for recommendations.

   Once you start to get email notifications, you can disable the automation by selecting the workflow and clicking on **Disable**.

   > Please be aware that if your trigger is a recommendation that has "sub-recommendations" / "nested recommendations", the logic app will not trigger for every new security finding when the status of the parent has changed.

5. Once the automation is automatically triggered, you should expect the email message to look like the screenshot below:

    ![Workflow automation generated email message](../Images/m5ex3step5.png)

6. Test/trigger your automation manually:

   - On the Microsoft Defender for Cloud panel, click on **Recommendations (1)** from the **General** section.
   - **Search(2)** and select **Azure Kubernetes Service clusters should have the Azure Policy Add-on for Kubernetes installed (3)** and click on it.
   
      > Note: If you don't see the above recommendation that means it is not loaded yet and it could take up to 24 hours for all the recommendations to show up. It is possible that during lab time, this may not show up – which is the case sometimes. You can note down this step number then continue to the next exercise and verify this later.

     ![](../Images/Im1.png)
     
   - In **Take action** tab under **Workflow automation** click on the **Trigger Logic App** button.

      ![](../Images/Im2.png)
     
   - In the Trigger a logic app blade, select the Logic App you created in the previous step (Send-RecommendationsChanges<inject key="DeploymentID" enableCopy="false"/>) then click on **Trigger**.

       ![](../Images/Im3.png)
     
    - You should receive an email, verifying in your inbox. On the labvm-xxxxxx open a new tab in the web browser and navigate to https://outlook.office365.com.

<validation step="845d2579-8c67-4525-a137-b105568741c7" />

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
 
- Navigate to the Lab Validation Page, from the upper right corner in the lab guide section.
- Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
- If not, carefully read the error message and retry the step, following the instructions in the lab guide.
- If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.
    
### Exercise 3: Accessing your secure score via ARG
Azure Resource Graph (ARG) provides an efficient and performant resource exploration with the ability to query at scale across a given set of subscriptions.

In this exercise, you will query and calculate your score for the security controls and accurately calculate the aggregated score across multiple subscriptions.

1. Search for **Resource Graph Explorer** in the search box located on the top of the **Azure Portal** page and click on **Resource Graph Explorer**.

    ![Resource Graph Explorer](../Images/m5ex4step1.png)

2. Paste the following KQL query and then select **Run query**.

     ```
     SecurityResources
     | where type == 'microsoft.security/securescores'
     | extend current = properties.score.current, max = todouble(properties.score.max)
     | project subscriptionId, current, max, percentage = ((current / max)*100)
     ```

    ![](../Images/run-query1.png)

   > **Note:** It could require up to few hours for ARG to provide the information. If you don't see any result, please return later to check again.

3. You should now see your subscription ID listed here, along with the current score (in points), the max score and the score in percentage.

4. To return the status of all the security controls, select **New query**. Next, paste the following KQL query and click on **Run query**:

     ```
     SecurityResources
     | where type == 'microsoft.security/securescores/securescorecontrols'
     | extend SecureControl = properties.displayName, unhealthy = properties.unhealthyResourceCount, currentscore = properties.score.current, maxscore = properties.score.max
     | project SecureControl , unhealthy, currentscore, maxscore
     ```

     ![](../Images/run-query2.png)

   > **Note:** It could require up to few hours for ARG to provide the information. If you don't see any result, please return later to check again.

More details on the [official article](https://docs.microsoft.com/en-us/azure/security-center/secure-score-security-controls) or on the [blog post](https://techcommunity.microsoft.com/t5/azure-security-center/querying-your-secure-score-across-multiple-subscriptions-in/ba-p/1749193)


## Summary

In this module, you have completed exploring more **Microsoft Defender for Cloud** features - **Vulnerability assessment for Containers**, **Automated recommendations with workflow automation** and **Accessed your secure score via ARG**.

Now you can move on to the next module by clicking on the Next button at the bottom right of the screen.
