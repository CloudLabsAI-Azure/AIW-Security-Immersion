# Module 8 – Advance Cloud Defense

### Overview

In this module, you will be exploring the Microsoft Defender for Cloud features for Advanced Cloud Defense

## Objectives

You will be performing the following activities to achieve the goal:

* Exercise 1: Using JIT to reduce the attack surface
* Exercise 2: Adaptive Application Control
* Exercise 3: File Integrity Monitoring

### Exercise 1: Using JIT to reduce the attack surface

In the simplest terms, the “attack surface” is the sum total of resources exposed to exploit within your enterprise. Defending the attack surface was a lot less complicated when a defined corporate “perimeter” existed, neatly separating a company’s assets from the outside world using **Just-in-time VM access**.

In this exercise, you will be using Just In Time access (JIT) to access your virtual machine.

1. Launch **Azure Portal** using the desktop icon on the **labvm-xxxxxx** and log in with the Azure credentials from the Lab **Environment Details** tab.

1. Type **Microsoft Defender for Cloud** in the search box located on the top of the **Azure Portal** page and click on it.

    ![](../Images/hyb-ex1-g1.png)

1. Select **Workload protections** under **Cloud Security** from the left side pane.

    ![](../Images/hyb-ex6-g23.png)

1. When you are on the **Just-in-time VM access** page, select the **Not configured** tab. You should see virtual machines listed: `asclab-linux` and `asclab-win`.
    
    > **Note**: If the virtual machines `asclab-linux` and `asclab-win` are present under the **Unsupported** tab, then follow the below instructions to enable **Just-in-time VM access**.
    ![](../Images/hyb-ex6-g24.png)

1. Navigate to **asclab** resource group and select **asclab-win** virtual machine.

    ![](../Images/hyb-ex6-g26.png)

    ![](../Images/hyb-ex6-g27.png)

1. Select **Configuration** from the left-hand side menu in **Settings** and click on **Enable Just-in-time**
       
    ![](../Images/hyb-ex6-g28.png)
       
1. Navigate back to **Microsoft Defender for Cloud** and select **Workload protections** under **Cloud Security** from the left side pane, then click on **Just-in-time VM access**.

    - Review the **Configured** tab, now you should see your VM configured: `asclab-win`

        ![](../Images/justintime1.png)
    
1. Select **asclab-win** and then click on the **Enable JIT on 1 VM** button.
    > If you have followed the above instructions to enable **Just-in-time VM access**, you can skip Steps 5-7 and continue from Step 13.
    
    ![Enable JIT on Windows VM](../Images/lab8-2.png)

1. On the **JIT VM access configuration** page, keep just the **3389 (RDP) port** and remove all the other ports listed. To remove, click on the ellipses icon (...) for each port and then click on **Delete**.

1. Click **Save** to apply the VM access configuration.

    ![JIT VM access configuration](../Images/asc-jit-vm-access-config.gif?raw=true)

1. Review the **Configured** tab, now you should see your VM configured: `asclab-win`.

1. Type **Virtual machines** in the search box located at the top of the Azure Portal page and click on it.

1. Select the virtual machine **asclab-win**.

    ![](../Images/hyb-ex6-g27.png)

1. On the VM **Overview** page, if the virtual machine is in a stopped state, click **Start** to power it on.

    ![](../Images/hyb-ex6-g31.png)

1. On the VM **Overview** page, click **Connect (1)** and select **Connect (2)** from the dropdown.

    ![](../Images/hyb-ex6-g32.png)

1. On the **Native RDP** page, click **Download RDP file** to download the connection file.

     ![Windows VM - Connect RDP](../Images/hyb-ex6-g33.png)

    > **Note**: If you get a Downloads notification, select **Keep**

     ![download-anyway](../Images/lab8-7.png)

1. Click on the downloaded file to initiate a remote connection to the server. On the warning message, ignore the message by clicking on **Connect**.

    ![](../Images/hyb-ex6-g34.png)

1. You should see the following error message: *Remote Desktop can't connect to the remote computer*. In this scenario, remote access to the server is not enabled. Close the popup window to continue.

    ![](../Images/hyb-ex6-g35.png)

1. Return to the VM blade **Connect** page, click on **Request access** under **Request just-in-time access**, select **Local machine IP** and then click on **Request access**. The access should be approved in a minute. 

     ![request-access](../Images/hyb-ex6-g36.png)
    
1. Verify that **JIT access** is granted and **port 3389** is accessible from the source IP, as indicated by the green checks.

    ![](../Images/hyb-ex6-g37.png)

1. Try to connect again to validate your JIT access to the VM. Use the same file you downloaded previously.

    ![](../Images/hyb-ex6-g34.png)

1. When the Windows Security prompt appears, click **More choices** to select a different account.

    ![](../Images/hyb-ex6-g38.png)

    ![](../Images/hyb-ex6-g39.png)

1. Now you should get the prompt for the local admin credentials. Login using the below credentials.
 
      - **VM Username**: .\demouser
      - **VM Password**: <inject key="VM Password"></inject>

          ![](../Images/hyb-ex6-g40.png)

1. When the certificate warning appears, click **Yes** to continue connecting to the virtual machine.

    ![](../Images/hyb-ex6-g41.png)

1. You **are now connected to asclab-win** server. Close the remote control session/log off.

    ![](../Images/hyb-ex6-g42.png)

### Exercise 2: Adaptive Application Control

Application control helps you deal with malicious and/or unauthorized software, by allowing only specific applications to run on your machines.

In this exercise, you will be using adaptive control in workload protection in Microsft defender for cloud.

1. Type **Microsoft Defender for Cloud** in the search box located on the top of the **Azure Portal** page and click on it, then select **Workload protections** under **Cloud Security** from the left side pane.

1. Navigate to the bottom section under Advanced protection, click on **Adaptive application control**

    ![Adaptive Application Control1](../Images/m8ex2.step2.png)

1. The Adaptive application controls page opens with your VMs grouped into the following tabs: Configured, Recommended and No Recommendation.

1. Click on the **Recommended** tab.

    ![Adaptive Application Control2](../Images/lab8-8.png)

    >**Note:** First-time users will not get any group information under the Group Name section. This is because Microsoft Defender for Cloud needs at least two weeks of data to define the unique recommendations per group of machines. 

### Exercise 3: File Integrity Monitoring

File integrity monitoring (FIM), also known as change monitoring, examines operating system files, Windows registries, application software, Linux system files, and more. It detects and reports changes that might indicate an attack.

In this exercise, you will be working with the file integrity monitoring under workload protection in Microsft defender for cloud.

It maps the current state of these items with the state during the previous scan and alerts you if any suspicious modifications have been made. To enable FIM, follow the instructions below:

1. Type **Microsoft Defender for Cloud** in the search box located on the top of the **Azure Portal** page and click on it, then select **Workload protections** under **Cloud Security** from the left side pane.

1. Navigate to the bottom section under Advanced Protection, and click on the **File Integrity Monitoring** tile.

    ![File Integrity Monitoring1](../Images/m8ex3.step2.png)

1. On the **File Integrity Monitoring** page, select the listed **Log Analytics workspace** named **asclab-la-<inject key="DeploymentID" enableCopy="false"/>** (or just by clicking on the Enable button - it indicates that File Integrity Monitoring is not enabled for the selected workspace).

   > **Note**: Deployment ID can be obtained from the Lab Environment output page.

   ![](../Images/FIM.png)

1. On the Enable File Integrity Monitoring window, review the default **recommended settings** for Windows files, Registry, and Linux files.

1. Click on the **Enable File Integrity Monitoring** button.

    ![File Integrity Monitoring2](../Images/m8ex3.step5.png)

<validation step="1e2354f0-1f25-4c38-a196-008d267eca18" />

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
 
- Navigate to the Lab Validation Page, from the upper right corner in the lab guide section.
- Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
- If not, carefully read the error message and retry the step, following the instructions in the lab guide.
- If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.
    
## Summary

In this module, you have completed exploring different **Microsoft Defender for Cloud** features - **Used JIT to reduce the attack surface**, **Adaptive Application Control** and **File Integrity Monitoring**. You have reached the end of the lab.
