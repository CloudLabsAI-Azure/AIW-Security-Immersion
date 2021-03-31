# Module 4 - Regulatory Compliance

### Overview

In this exercise, you will learn about Regulatory Compliance features

You will be performing the following activities to achieve the goal.

* Exploring Regulatory Compliance dashboard
* Adding new standards to Compliance policies
* Creating custom benchmark

### Exercise 1: Understanding Regulatory Compliance dashboard

1.	Launch **Azure Portal** using the desktop icon on the **JumpVM** and login with the Azure credentials from the Lab **Environment Details** tab if you are not logged in already.

2.	Type **Security Center** in the search box located on the top of the **Azure Portal** page and click on it. Next, select **Regulatory Compliance** tile (this pilar is also available from the left sidebar).

3.	Once the Regulatory Compliance dashboard opens you can see the compliance standards currently assigned to your subscription.

4.	On the top strip, notice the number of **Passed vs. failed controls** across standards.

![Regulatory compliance assessment and standards](../Images/asc-regulatory-compliance-assessment-standards.png)

5.	On the main page, select **ISO 27001** standard. Notice the different compliance controls mapped to assessments.

6.	Locate and expand the **A13 Communications security** compliance control. Click on the compliance domain **A13.2. Information transfer** and expand **A13.2.1. Information transfer policies and procedures** – Observe both _failed_ status.

![Remmediate function app](../Images/communications-security.png)

7.	You can also remediate assessments in this section. Click on the first assessment **Function App should only be accessible over HTTPS**.

8.	On the recommendation *Function App should only be accessible over HTTPS*, select the unhealthy resource (asclab-fa-xxx here xxx is the unique ID) and click on **Remediate**. Confirm the action by selecting **Remediate 1 resource**.

![Remmediate function app](../Images/asc-remmediate-function-app.gif?raw=true)

9.	Return to the dashboard. Here, you can export the regulatory standard compliance status report as a PDF or CSV file. From the top menu bar, click on **Download report**.

10.	On the Report standard dropdown menu, select **PCI DSS 3.2.1** and **PDF**. Click on **Download**

11.	A local PDF file is now stored on your machine. Open the **PCI DSS 3.2.1 Compliance Report** and explore it – This report summarizes the status of those assessments on your environment, as mapped to the associated controls.

### Exercise 2: Adding new standards

You can add additional industry standards (represented as compliance packages) such as IST SP 800-53 R4, SWIFT CSP CSCF-v2020, UK Official and more.

1.	Type **Security Center** in the search box located on the top of the **Azure Portal** page and click on it. Next, select **Regulatory Compliance** from the left sidebar. Now select **Manage compliance policies** from the top menu bar.

![Manage compliance policies](../Images/manage-compliance-policies.png)

2.	Select a scope to assign the new package: **Your Subscription**.

3.	In the **Industry & regulatory standards** section, notice the out of the box standards. Click on **Add more standards**.

4.	On the **Add regulatory compliance standards** window, locate the **Azure CIS 1.1.0** standard and click on **Add**.

![Manage compliance policies](../Images/add-more-standards.png)

5.	Click on **Review + create** and then **Create**.

![Review + create](../Images/add-more-standards-create.png)

> ❗ Important: <br>
> It will take a while until the change takes an effect (approximately 2-3 hours).

6.	**Azure CIS 1.1.0 (New)** should now be listed on the standards list.

![Add CIS 1.1.0 (New) Standard](../Images/asc-azure-cis-new-standard.gif?raw=true)

### Exercise 3: Creating your own benchmark

Once you create your custom initiative, ASC allows you to add it as a security policy and provides two main benefits:
* Security requirements represented as custom recommendations, listed under the recommendation list.
* Track compliance status using regulatory compliance dashboard.

Type **Policy** in the search box located on the top of the **Azure Portal** page and click on it. Alternately, you can navigate to the policy section by clicking on this [link](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/Overview).

1.	From the left pane, select **Definitions**.

2.	From the top menu, select **+ initiative definition** to create a new policy set definition.

![Benchmark Policy](../Images/benchmark-policy.png)

3.	Under the **Basics** tab, select your Subscription.

4.	Select a name, for example: **Custom Benchmark**.

5.	Provide an informative description so others can be clear on what is the purpose of this new security policy.

6.	Select **Category**. You can decide to use existing one (for example: Security Center) or to create your own one. *The recommended approach is to use a custom one so you can quickly filter policy definitions and initiatives when needed (for example: Contoso)*.

7.	Provide **Version** number. Each policy definition and initiative contain a version in its metadata section. You can decide to have major versions (1.0), minor version (1.1) and so.

![Benchmark Next](../Images/benchmark-create.png)

8.	On the **Initiative definition** blade click on **Groups**, in this section you can define your groups and subgroups to be used in your initiative. To add a new group, click on **Create Group**.

9.	Once you do that, you will be able to create a New Group. For this demonstration, we will name it **Group 1**. Next, click on **Create new** under Subgroup and name it **Sub-group1** and provide a description. Please note that additional metadata can be used as well. The location of the policyMetadata object that has additional details about the control and compliance domain. Click on **Save** to create the new group.

![Group create](../Images/group-policy.png)

10.	Repeat the process to create additional group, for example: **Group 2**.

11.	Now you should have two groups to help you organize your policies within the initiative.

12.	On the **Initiative definition** blade, click on the **Policies** tab. Here you can add policy definitions, both built-in and custom. Click **Add policy definition(s)**. Select your desired polices, if you create a benchmark, you can also leverage existing policy definitions from **Microsoft managed** tab. For example, you can choose the following policies and select Add:
    -	Audit virtual machines without disaster recovery configured
    -	Azure Backup should be enabled for Virtual Machines
    -	Audit VMs that do not use managed disks

![Group create](../Images/add-policy.png)

13.	Every policy on the list, has its definition name, reference ID and the associated group. However, you do need to define a group for each policy. To do so, click on the **…** to open the context menu and select **Edit groups**.

14.	Make sure all policies are associated to a group. Please notice that policies can be associated to multiple groups. Here we are selecting **Group 1** and select **Save**.

![edit group](../Images/edit-group.png)

![edit group](../Images/edit-group1.png)

15.	You can assign policy and initiative parameters to be used during the assignment process. Skip this section and click on **Review + Create** to validate your settings. Then, click on **Create**

16.	You should now see your new initiative listed here – **Custom Benchmark** along with the additional metadata (scope, category, etc.)

17.	To assign your new security policy, type **Security Center** in the search box located on the top of the **Azure Portal** page and click on it.

18.	From the left navigation pane, under **Management** section, click on **Security policy**.

19.	Select a **Subscription** to assign your new security policy.

![security policy](../Images/security-policy.png)

20.	On **Security policy** page, navigate to **Your custom initiatives** section and select **Add a custom initiative**. 

![Add a custom initiative](../Images/add-a-custom-initiative.png)

21.	On **Add custom initiative** window, your new standard should be listed. Now you can click on **Add** to assign to it. Once assigned, it will be listed in the Recommendations blade and will be added in the **Regulatory Compliance** dashboard too.

![Custom Initiative](../Images/custom-initiative.png)

22.	Follow the **on-screen instructions to assign it on the desired scope**. If you decide to include parameters in your initiative here is where you can do it. Click on **Review + create** to start the validation process and then click on **Create**.

23.	Now your new security benchmark is displayed in regulatory compliance along with the built-in regulatory standards.

### Summary

In this module, you have completed Exploring **Security Center** features - **Regulatory Compliance dashboard**, **Added new standards** and **Created your own benchmark**.

Now you can move on to the next module by clicking on the Next button at the bottom right of the screen.
