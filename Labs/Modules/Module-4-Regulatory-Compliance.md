# Module 4 - Regulatory Compliance

### Overview

In this exercise, you will learn about Regulatory Compliance features

You will be performing the following activities to achieve the goal.

* Exploring Regulatory Compliance dashboard
* Adding new standards to Compliance policies
* Creating custom benchmark

### Exercise 1: Understanding Regulatory Compliance dashboard

Azure Security Center helps streamline the process for meeting regulatory compliance requirements, using the regulatory compliance dashboard. The regulatory compliance dashboard shows the status of all the assessments within your environment for your chosen standards and regulations. As you act on the recommendations and reduce risk factors in your environment, your compliance posture improves.

Security Center continuously assesses your hybrid cloud environment to analyze the risk factors according to the controls and best practices in the standards applied to your subscriptions.

1.	Navigate to Security Center in the Azure portal(perform if not already on the Security center page).

2.	On the overview page select the **Regulatory Compliance(1)** tile (this pilar is also available on the left side under the Cloud Security section).

3.	Once the **Regulatory Compliance dashboard(2)** opens you can see the compliance standards currently assigned to your subscription.

   ![](../Images/m4ex1.step3.png)

4.	On the top strip, notice the number of **Passed vs. failed controls** across standards.

![Regulatory compliance assessment and standards](../Images/asc-regulatory-compliance-assessment-standards.png)

5.	On the main page, select **ISO 27001** standard. Notice the different compliance controls mapped to assessments.

6.	Locate and expand the **A13 Communications security** compliance control. Click on the compliance domain **A13.2. Information transfer** and expand **A13.2.1. Information transfer policies and procedures** – Observe both _failed_ status.

   ![Remmediate function app](../Images/m4ex1step6.png)

7.	You can also remediate assessments in this section. Click on the first assessment **Function App should only be accessible over HTTPS**.

8.	On the recommendation *Function App should only be accessible over HTTPS*, select the unhealthy resource under the Affected resources named **<inject key="Function App" props="{\&quot;enableCopy\&quot;:true,\&quot;style\&quot;:{\&quot;fontWeight\&quot;:\&quot;bold\&quot;}}" />** and click on **Fix**. Confirm the action by selecting **Fix 1 resource**.

   ![Remmediate function app](../Images/asc-remmediate-function-app.png)

9.	Return to the dashboard. Here, you can export the regulatory standard compliance status report as a PDF or CSV file. From the top menu bar, click on **Download report**.

10. On the Report standard dropdown menu, select **PCI DSS 3.2.1** and format as **PDF**. Click on **Download**

11. A local PDF file is now stored on your machine. Open the **PCI DSS 3.2.1 Compliance Report** and explore it – This report summarizes the status of those assessments on your environment, as mapped to the associated controls.

### Exercise 2: Adding new standards

You can add additional industry standards (represented as compliance packages) such as IST SP 800-53 R4, SWIFT CSP CSCF-v2020, UK Official and more.

1.	On **Regulatory Compliance** page, select **Manage compliance policies** from the top menu bar.

    ![Manage compliance policies](../Images/manage-compliance-policies.png)

2.	Select **Your Subscription** under the Policy management header.

   ![](../Images/m4ex2step2.png)

3.	In the **Industry & regulatory standards** section, notice the out of the box standards. Click on **Add more standards**.

   ![](../Images/m4ex2step3.png)
   
4.	On the **Add regulatory compliance standards** window, locate the **Azure CIS 1.1.0** standard and click on **Add**.

    ![Manage compliance policies](../Images/add-more-standards.png)

5.	Click on **Review + create** and then **Create**.

    ![Review + create](../Images/add-more-standards-create.png)

> ❗ Important: <br>
> It will take a while until the change takes an effect (approximately 2-3 hours).

6.	**Azure CIS 1.1.0 (New)** should now be listed on the standards list.

    ![Add CIS 1.1.0 (New) Standard](../Images/m4ex2step6.png)

### Exercise 3: Creating your own benchmark

Once you create your custom initiative, ASC allows you to add it as a security policy and provides two main benefits:
* Security requirements represented as custom recommendations, listed under the recommendation list.
* Track compliance status using regulatory compliance dashboard.

1. In the search box located on the top of the Azure Portal page, search for Policy and click on it.

   ![Add CIS 1.1.0 (New) Standard](../Images/m3ex2.step1.png)

2.	From the left pane of the **Policy** page, select **Definitions**.

3.	From the top menu, select **+ initiative definition** to create a new policy set definition.

    ![Benchmark Policy](../Images/benchmark-policy.png)

4.	Under the **Basics** tab, select your Subscription.

5.	Provide **Custom Benchmark** as Name.

6.	Enter **Custom Benchmark Policy** as Description.

7.	Select **Category**. Here, you can use an existing one (for example: Security Center).

8.	Provide **Version** number. Each policy definition and initiative contain a version in its metadata section. You can decide to have major versions (1.0), minor version (1.1) and so.

   ![Benchmark Next](../Images/benchmark-create.png)

9.	On the **Initiative definition** blade click on **Groups**, in this section you can define your groups and subgroups to be used in your initiative. To add a new group, click on **Create Group**.

10. Once you do that, you will be able to create a New Group. For this demonstration, we will name it **Group 1**. Next, click on **Create new** under Subgroup and name it **Sub-group1** and provide a description. Please note that additional metadata can be used as well. The location of the policyMetadata object that has additional details about the control and compliance domain. Click on **Save** to create the new group.

![Group create](../Images/group-policy.png)
  
11. Repeat the process to create an additional group, for example: **Group 2**.

12. Now you should have two groups to help you organize your policies within the initiative.

13. On the **Initiative definition** blade, click on the **Policies** tab. Here you can add policy definitions, both built-in and custom. Click **Add policy definition(s)**. Select your desired polices, if you create a benchmark, you can also leverage existing policy definitions from **Microsoft managed** tab. For example, you can choose the following policies and select **Add**:
    -	Audit virtual machines without disaster recovery configured
    -	Azure Backup should be enabled for Virtual Machines
    -	Audit VMs that do not use managed disks

![Group create](../Images/add-policy.png)

14. Every policy on the list, has its definition name, reference ID and the associated group. However, you do need to define a group for each policy. To do so, click on the **… (1)** to open the context menu and select **Edit groups (2)**.

   ![edit group](../Images/edit-group.png)

15. Make sure all policies are associated to a group. Please notice that policies can be associated to multiple groups. Here we are selecting **Group 1 (1)** and select **Save (2)**.

    ![edit group](../Images/edit-group1.png)

16. You can assign policy and initiative parameters to be used during the assignment process. Skip this section and click on **Review + Create** to validate your settings. Then, click on **Create**

17. You should now see your new initiative listed here – **Custom Benchmark** along with the additional metadata (scope, category, etc.)

18. To assign your new security policy, type **Security Center** in the search box located on the top of the **Azure Portal** page and click on it.

19. From the left navigation pane, under the **Management** section, click on **Security policy (1)**.

20. Select a **Subscription (2)** to assign your new security policy.

  ![security policy](../Images/security-policy.png)

21. On the **Security policy** page, navigate to the **Your custom initiatives** section and select **Add a custom initiative**. 

  ![Add a custom initiative](../Images/add-a-custom-initiative.png)

22. On **Add custom initiative** window, your new standard should be listed. Custom Benchmark initiative can be added by clicking on **Add** button. Once assigned, it will be listed in the Recommendations blade and will be added in the **Regulatory Compliance** dashboard too.

  ![Custom Initiative](../Images/custom-initiative.png)

23. Follow the **on-screen instructions to assign it on the desired scope**. If you decide to include parameters in your initiative here is where you can do it. Click on **Review + create** to start the validation process and then click on **Create**.

24. After some time your new custom benchmark is displayed in Regulatory compliance dashboard along with the built-in regulatory standards.

### Summary

In this module, you have completed Exploring **Security Center** features - **Regulatory Compliance dashboard**, **Added new standards** and **Created your own benchmark**.

Now you can move on to the next module by clicking on the Next button at the bottom right of the screen.
