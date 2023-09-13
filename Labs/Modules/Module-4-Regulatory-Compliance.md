# Module 4 - Regulatory Compliance

### Overview

In this exercise, you will learn about Regulatory Compliance features

You will be performing the following activities to achieve the goal.

* Exploring Regulatory Compliance dashboard
* Adding new standards to Compliance policies
* Creating a custom benchmark

### Exercise 1: Understanding Regulatory Compliance dashboard

Microsoft Defender for Cloud helps streamline the process for meeting regulatory compliance requirements, using the regulatory compliance dashboard. The regulatory compliance dashboard shows the status of all the assessments within your environment for your chosen standards and regulations. As you act on the recommendations and reduce risk factors in your environment, your compliance posture improves.

Microsoft Defender for Cloud continuously assesses your hybrid cloud environment to analyze the risk factors according to the controls and best practices in the standards applied to your subscriptions.

1. Navigate to **Microsoft Defender for Cloud** in the Azure portal(perform if not already on the Microsoft Defender for Cloud).

1. On the overview page select the **Regulatory Compliance (1)** tile (this pillar is also available on the left side under the Cloud Security section). Once the **Regulatory Compliance dashboard (2)** opens you can see the compliance standards currently assigned to your subscription.

    ![](../Images/c11.png)

1. On the main page, select the **Contoso Security Benchmark** standard. Notice the different compliance controls mapped to assessments.

   >Note: It might take up to 30 minutes to reflect the Contoso security benchmark after adding the custom initiatives. if this is not available for you, you can skip this exercise and continue with the next exercise and can check on this later.

    ![Contoso Security Benchmark](../Images/CSB.png)

1. Expand the **Contoso Security Benchmark** compliance control. Click on the **Managed identity should be used in your function app**

    ![Remmediate function app](../Images/CSB1.png)
   
1. Under **Managed identity should be used in your function app** tab, expand **Affected resources**.

    ![](../Images/affectedresources1.png)
   
1. Now under **Healthy resources (1)**, you can observe the **Function app (2)**.

    ![](../Images/healthyresources.png)

1. Return to the dashboard. Here, you can export the regulatory standard compliance status report as a PDF or CSV file. From the top menu bar, click on **Download report**.

    ![](../Images/downloadreport.png)

1. On the Report standard dropdown menu, select **Microsoft cloud security benchmark** and format as **PDF*. Click on **Download**.

    ![](../Images/c12.png)

1. A local PDF file is now stored on your machine. Open the **Microsoft Cloud security benchmark Compliance Report** and explore it – This report summarizes the status of those assessments on your environment, as mapped to the associated controls.

### Exercise 2: Adding new standards

You can add additional industry standards (represented as compliance packages) such as IST SP 800-53 R4, SWIFT CSP CSCF-v2020, UK Official and more.

1. On **Regulatory Compliance** page, select **Manage compliance policies** from the top menu bar.

    ![Manage compliance policies](../Images/c13.png)

2. Select **Your Subscription** under the Environment settings.

    ![](../Images/envset.png)
   
3. Under **Policy Settings** tab, select **Security Policy (1)**, then expand **Industry & regulatory standards** and click on **Add more standards (2)**.

    ![](../Images/security-policy-standards.png)
   
4. On the **Add regulatory compliance standards** window, locate the **CIS Azure Foundations v1.1.0** standard and click on **Add**.

    ![Manage compliance policies](../Images/Sh2.png)

5. Click on **Review + create** and then **Create**.

   >Note: If it fails to create then please click on the previous button on the deployment page and start the deployment again.

    ![Review + create](../Images/neew6.png)

  > ❗ Important: <br>
  > It will take a while until the change takes effect (approximately 2-3 hours).

6. **CIS Azure Foundations v1.1.0** should now be listed on the standards list.

     ![Add CIS 1.1.0 (New) Standard](../Images/Sh3.png)

### Exercise 3: Creating your own benchmark

Once you create your custom initiative, Microsoft Defender for Cloud allows you to add it as a security policy and provides two main benefits:
* Security requirements represented as custom recommendations, listed under the recommendation list.
* Track compliance status using the regulatory compliance dashboard.

1. In the search box located at the top of the Azure Portal page, search for Policy and click on it.

    ![Add CIS 1.1.0 (New) Standard](../Images/m3ex2.step1.png)

1. From the left pane of the **Policy** page, select **Definitions**.

1. From the top menu, select **+ initiative definition** to create a new policy set definition.

    ![Benchmark Policy](../Images/benchmark-policy.png)

1. Under the **Basics** tab, enter the following steps:

   - Initiative Location: Select your **Subscription (1)**
    
   - Name: Enter **Custom Benchmark (2)**

   - Description: Enter **Custom Benchmark Policy (3)**

   - Category: Click **Use existing (4)** and Select **Security center (5)** from drop-down list.

   - Click on **Next (7)**

    ![Benchmark Next](../Images/Sh4.png)

1. On the **Initiative definition** blade click on **Groups**, In this section you can define your groups and subgroups to be used in your initiative. To add a new group, click on **Create Group**.

    ![](../Images/creategroup.png)
   
1. Under **Create group**, enter the following details:

    - Name: **Group-1 (1)**
    - Display name: **Group-1 (2)**
    - Subgroup: Click on **Create new (3)** and enter the name as **Sub-group1 (4)**. You can also provide a description. Please note that additional metadata can be used as well. The location of the policy metadata object that has additional details about the control and compliance domain.
    
    - Click on **Save (5)** to create the new group.  

     ![Group create](../Images/createagroup.1.png)
  
1. Repeat the process to create an additional group, for example, **Group 2**.

1. Now you should have two groups to help you organize your policies within the initiative.

1. On the **Initiative definition** blade, click on the **Policies** tab. Here you can add policy definitions, both built-in and custom. Click **Add policy definition(s)**. Select your desired policies, If you create a benchmark, you can also leverage existing policy definitions from the **Microsoft managed** tab. For example, you can choose the following policies and select **Add**:
    -	Audit virtual machines without disaster recovery configured
    -	Azure Backup should be enabled for Virtual Machines
    -	Audit VMs that do not use managed disks

     ![Group create](../Images/policydef.png)

1. Every policy on the list, has its definition name, reference ID and the associated group. However, you do need to define a group for each policy. To do so, click on the **… (1)** to open the context menu and select **Edit groups (2)**.

    ![edit group](../Images/edit-group.png)

1. Make sure all policies are associated with a group. Please notice that policies can be associated with multiple groups. Here we are selecting **Group 1 (1)** and selecting **Save (2)**.

     ![edit group](../Images/edit-group1.png)

1. You can assign policy and initiative parameters to be used during the assignment process. Skip this section and click on **Review + Create** to validate your settings. Then, click on **Create**

1. You should now see your new initiative listed here – **Custom Benchmark** along with the additional metadata (scope, category, etc.)

    ![](../Images/customben.png)

1. To assign your new security policy, type **Microsoft Defender for Cloud** in the search box located at the top of the **Azure Portal** page and click on it.

    ![](../Images/m3e1s1.png)
     
1. From **Microsoft Defender for Cloud** blade, Select **Environment settings**. Here you'll be able to see the subscription.

    ![Template deployment completed](../Images/m2e1s3.2.png)
   
1. On the **Environment Settings** page, select your subscription.

    ![Template deployment completed](../Images/m1e2.1s2.png)
   
1. Under **Policy Settings** tab, select **Security Policy (1)**, then expand **Your custom initiatives** and click on **Add custom initiatives (2)**.

    ![](../Images/security-policy-custom.png)

1. On the **Add custom initiative** window, your new standard should be listed. Custom Benchmark initiative can be added by clicking on the **Add** button. Once assigned, it will be listed in the Recommendations blade and will be added to the **Regulatory Compliance** dashboard too.

    ![Custom Initiative](../Images/custom-initiative.png)

1. Follow the **on-screen instructions to assign it to the desired scope**. If you decide to include parameters in your initiative here is where you can do it. Click on **Review + create** to start the validation process and then click on **Create**.

1. After some time your new custom benchmark is displayed in the Regulatory compliance dashboard along with the built-in regulatory standards.

### Summary

In this module, you have completed Exploring **Microsoft Defender for cloud** features - **Regulatory Compliance dashboard**, **Added new standards** and **Created your own benchmark**.

Now you can move on to the next module by clicking on the Next button at the bottom right of the screen.
