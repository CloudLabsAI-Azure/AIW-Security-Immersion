# Module 3 - Security Policy


## Overview

In this module, we will guide you through the current Security Center policies set by Azure. Also, we will walk you through the methods to enable or disable the Security policies. 

### Exercise 1: Overview of the ASC policy

In this exercise, You will get an overview of an index of Azure Policy built-in policy definitions related to Azure Security Center and about initiatives, policies, and how they relate to the Security Center's recommendation.

1.  Launch **Azure Portal** using the desktop icon on the **labvm-xxxxxx** and login with the Azure credentials from the Lab **Environment Details** tab if not logged in already.

2.	Type **Security Center** in the search box located on the top of the **Azure Portal** page and click on it.

3.	Click on **Security policy** from the left navigation pane under the **Management** section.

4.	On the Policy Management page, select **Azure subscription**.

5.	By default, there is 1 assignment at the **Security center default policy** which is **ASC default**.

    ![Security center default policy](../Images/asc-default-policy-subscription.png)

Note: This policy is enabled by default on your subscription as per Azure Security Center recommendations. This is the default set of policies monitored by Azure Security Center. It is automatically assigned as part of onboarding to Security Center. The default assignment contains only audit policies. For more information, please visit https://aka.ms/ascpolicies.

6.	To view the policy, click on **ASC Default (subscription...)**.

> Note: the assignment name will have GUID of the subscription in your lab environment.

7.	On the **Edit Initiative Assignment** page, click on **Parameters**.

8.	On the **Network Security Groups on the subnet level should be enabled**, change the action to **AuditIfNotExists** to enable monitoring of NSGs on subnets.

9.	Click on **Review + save**.

10.	On the Review tab, you can see your changes under the Parameters section: **networkSecurityGroupsOnSubnetsMonitoringEffect: AuditIfNotExists**

    ![Modifying Security Center default policy assignment](../Images/asc-default-policy-nsg-recommendation.png)

11.	Click on **Save**. Wait for the policy update to complete successfully.

### Exercise 2: Explore Azure Policy

Azure Policy keeps track of compliance for your Azure resources based on policy definitions you assign, these are called policy assignments. By default, Microsoft provides many built-in definitions that you can leverage as you see fit.

1.	Type **Policy** in the search box located on the top of the **Azure Portal** page and click on it. Alternately, open a new browser tab in the **labvm-xxxxxx** and navigate to this link https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade.

2.	From the left navigation pane, under the **Authoring** section, click on **Definitions**. This is where you can explore the built-in policy definitions and initiatives.

3.	From the top menu, use the filter ribbon and select **Security Center** from the category filter and set the Definitions Type as **Initiative**

4.	You can now see two built-in initiatives used by Azure Security Center:
    -	*Azure Security Benchmark*
    -	*[Preview]: Enable Data Protection Suite*

    ![policy assignment](../Images/policy.png)

5.	Notice the number of policies included in each initiative (policies column)

6.	To see current assignments, click on **Assignments** from the left navigation pane under **Authoring**. Policy initiatives have a different name for the assignments, for example:

    - *ASC Default (subscription: dd82589b-444c-45a8-863a-816243ce017d)*

7.	Click on **ASC Default** to see the assignment details.

### Exercise 3: Create resource exemption for a recommendation

Resource exemption will allow increased granularity for you to fine-tune recommendations by providing the ability to exempt certain resources from evaluation.
When working with a recommendation, you can create an exemption by clicking the ellipsis menu on the right side and then select create an exemption.

Note: Exemptions is a premium Azure policy capability that's offered for Azure Defender customers with no additional cost. For other users, charges may apply in the future.

1.	Type **Security Center** in the search box located on the top of the **Azure Portal** page and click on it.

2.	Select **Recommendations** from the left navigation pane.

3.	Expand **Secure management ports** security control from the list.

4.	Select the **Management ports should be closed on your virtual machines** recommendation.

    ![policy assignment](../Images/secure-management-ports.png)

   **Note**: If you don't see the above option that means it is not loaded yet to the control list, Note down this step number and verify this after some time.

5.	On the list of **Unhealthy resources** under **Affected resources**, see the current resources: *asclab-win* and *asclab-linux*.

6.	Select the **asclab-win** resource and then click on **Exempt**.

    ![Create exemption](../Images/asc-management-ports-resource-exemption.gif?raw=true)

7.	The **Exempt pane** opens:
    - Name: **ASC-Management ports should be closed on your virtual machines**.
    - Check the **Set an expiration date** option and set datetime for two days ahead on 12:00 AM.
    - Select **Waiver** as exemption category.
    - Click on **Create**.

![Exempt tab](../Images/exempt-scope.png)

> ⭐ Good to know: <br>
> **Mitigated** - This issue isn't relevant to the resource because it's been handled by a different tool or process than the one being suggested
> **Waiver** - Accepting the risk for this resource

8.	It might take up to **30 min for the exemption to take effect**. Once this happens:
    - The resource doesn't impact your secure score.
    - The resource is listed in the Not applicable tab of the recommendation details page
    - The information strip at the top of the recommendation details page lists the number of exempted resources: **1**
    
    <br>

9.	Refresh tab and open the **Not applicable resources** tab to review your exempted resource – you can see our resource along with the reason/description value.

    ![Exempttion tab](../Images/not-applicable-resource-tab.png)

10.	Exemption rules are based on Azure Policy capability. Therefore, you can track all your exemptions from Azure Policy blade as well.

11.	Type **Policy** in the search box located on the top of the Azure Portal page and click on it. Next, select Exemptions from the left navigation pane. Notice your newly created exemption listed there.

    ![Exempttion tab](../Images/exemptions-policy.png)

### Exercise 4: Create policy enforcement and deny

In this exercise, you will learn how to use Azure Policy to do some of the more common tasks related to assigning, denying, and managing policies across your organization.

1.	Type **Security Center** in the search box located on the top of the Azure Portal page and click on it..

2.	From the left side pane of **Security Center**, select **Recommendations** under **General**.

3.	On recommendations filters, set the **Response actions** as **Deny**.

    ![Auditing on SQL server should be enabled](../Images/asc-recommendations-filters-deny.gif?raw=true)

4.	From the filtered recommendations list, select **Secure transfer to storage accounts should be enabled**.

5.	From the top menu bar, click on the **Deny** button. *Enforce and Deny options provide you another way to improve your score by preventing security misconfigurations*.

> ❗ Important: <br>
> Security misconfigurations are a major cause of security incidents.

  ![Secure Transfer](../Images/secure-transfer.png)

6.	On the **Deny - Prevent resource creation**, select your subscription (which is currently set to audit mode). This allows you to ensure that from now on, a storage account without the security transfer feature turned on will be denied. Click on **Change to Deny**.

    ![Prevent resource creation](../Images/asc-storage-deny-policy.gif?raw=true)

7.	Go back to the **recommendations view**, set the **Response action** filter as **Select All**. In the search box, type **Auditing**. Click on the recommendation **Auditing on SQL server should be enabled**.

    ![Auditing on SQL server should be enabled](../Images/asc-auditing-sql.gif?raw=true)

8.	On the **Auditing on SQL server should be enabled** page, from the top menu bar, click on the **Enforce** button. This option allows you to take advantage of Azure policy’s DeployIfNotExist effect and automatically remediate non-compliant resources upon creation.

9. Once the **Configure SQL servers to have auditing enabled** pane opens with all of the policy configuration options, select the following configuration settings:

* Under the **Basics** tab under the Scope header, select the ellipse icon (...) to select your subscription and click on the **Select**
* Then click on **Next**

  ![Sql Auditing](../Images/auditing-create.png)

10. Next, under the **Parameters** tab leave the retention days to default value populated and select the resource group **asclab** from the drop down menu.

* Select **Review + create** to assign the policy to your subscription.
* Click **Create**

  ![Sql Auditing](../Images/auditing-create1.png)

11. On the **Auditing on SQL server should be enabled** page, **select** the SQL Server resource found on the **unhealthy resources** tab of **Affected resources** named **<inject key="SQL Server" props="{\&quot;enableCopy\&quot;:true,\&quot;style\&quot;:{\&quot;fontWeight\&quot;:\&quot;bold\&quot;}}" />** and click **Fix**. Change the retention days parameter to 180 and then click **Fix 1 resource**. By doing both operations, you can now ensure your existing resources and new ones will be enabled for auditing. Auditing on your SQL Server helps you track database activities across all databases on the server and save them in an audit log.

    ![Sql Auditing](../Images/auditing-fix-create.png)

12.	[Click here](https://docs.microsoft.com/en-us/azure/security-center/prevent-misconfigurations#recommendations-with-denyenforce-options "Recommendations with deny/enforce options") to view a full list of recommendations with deny/enforce options along with a detailed explanation of this capability.

13.	[Click here](https://docs.microsoft.com/en-us/azure/security-center/secure-score-security-controls#security-controls-and-their-recommendations "Security controls and their recommendations") to review a list of security controls and their recommendations.

### Exercise 5: Create a custom policy

A custom policy definition allows customers to define their own rules for using Azure. Whatever the business driver for creating a custom policy, the steps are the same for defining the new the custom policy.

***Create a custom initiative using Azure Policy***

1.	Type Policy in the search box located on the top of the Azure Portal page and click to open it or navigate to https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade

2.	Select **Definitions** from the left navigation pane.

3.	From the top menu, select **+Initiative definition** to add a new initiative

4.	On the New Initiative definition page, select the following:
    - Initiative location: Your Subscription
    - Name: **Contoso Security Benchmark**
    - Description: Baseline for security policies to appear alongside the built-in recommendations
    - Category: select Create new and type: **Contoso**
    - Version: **1**
    - Click **Next**
  
    ![Policy initiative definition settings page](../Images/asc-new-policy-initiative-definition.gif?raw=true)

5.	On the Policies tab, select **Add policy definitions**.

6.	The Add policy definition(s) pane opens: <br>
Add each policy one by one:
      Search and select the below policy definitions and Click on **Add**
    - *Managed identity should be used in your Function App*
    - *Custom subscription owner roles should not exist*
    - *Public network access on Azure SQL Database should be disabled*
    - *SSH access from the Internet should be blocked*
    - *Storage accounts should restrict network access*

7. Select **Review + Create** and click on **Create**.

   ![custom initiative](../Images/policy-definition.png)

***Add a custom initiative to your subscription***

1.	Type **Security Center** in the search box located on the top of the **Azure Portal** page and click to open it then from the left side pane under the **Management** section select **Security policy**.

2.	Select your subscription as a scope for your custom initiative.

   > Note: You must add custom standards at the subscription level (or higher) for them to be evaluated and displayed in Security Center.

3.	On the Security policy page, under **Your custom initiatives**, click **Add a custom initiative**.

    ![Add custom initiative](../Images/custom-initiatives.png)

4.	Your newly created initiative is listed: **Contoso Security Benchmark**. Select **Add**.

    ![Assign custom initiative](../Images/asc-assign-custom-initiative.gif?raw=true)

5.	On the **Assign Initiative** page, select **Review + Create** and then **Create**.

6.	Your custom initiative is now assigned.

### Summary

In this module, you have completed Exploring **Security Center** features, **ASC default policy, Azure Policy, Created resource exemption, Created policy enforcement and deny,** and **Created custom policy**.

Now you can move on to the next module by clicking on the Next button at the bottom right of the screen.
