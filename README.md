# Create Network Security Group

The Virtual Network is in place and divided into subnets — now it's time to secure it! In this task, you will create network security groups for the TODO web app. 

## Prerequisites

Before completing any task in the module, make sure that you followed all the steps described in the **Environment Setup** topic, in particular: 

1. Ensure you have an [Azure](https://azure.microsoft.com/en-us/free/) account and subscription.

2. Create a resource group called *“mate-resources”* in the Azure subscription.

3. In the *“mate-resources”* resource group, create a storage account (any name) and a *“task-artifacts”* container.

4. Install [PowerShell 7](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell?view=powershell-7.4) on your computer. All tasks in this module use PowerShell 7. To run it in the terminal, execute the following command:

    ```
    pwsh
    ```

5. Install [Azure module for PowerShell 7](https://learn.microsoft.com/en-us/powershell/azure/install-azure-powershell?view=azps-11.3.0): 
    ```
    Install-Module -Name Az -Repository PSGallery -Force
    ```
If you are a Windows user, before running this command, please also run the following: 
    ```
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ```

6. Log in to your Azure account using PowerShell:
    ```
    Connect-AzAccount -TenantId <your Microsoft Entra ID tenant id>
    ```

## Requirements

In this task, you will need to plan and create network security groups for the virtual network from the [previous task](https://github.com/mate-academy/azure_task_15_create_virtual_network): 

- each subnet (`webservers`, `database`, `management`) should have its own NSG, with the same name as the subnet;
- all subnets should allow traffic from other subnets within the virtual network;
- `webservers` subnet should accept only HTTP and HTTPS traffic from the Internet;
- `management` subnet should accept only SSH traffic from the Internet; 
- `database` subnet should not accept any traffic from the Internet at all.

To complete the task, you need to perform the following steps: 

1. Update the PowerShell script `task.ps1` to add deployment of the required Network Security Groups and subnets using the PowerShell module for Azure. To achieve that, use comandlets [New-AzNetworkSecurityGroup and New-AzNetworkSecurityRuleConfig](https://learn.microsoft.com/en-us/powershell/module/az.network/new-aznetworksecuritygroup?view=azps-12.1.0#example-2-create-a-detailed-network-security-group). File `task.ps1` already contains code for deployment of the virtual network and subnets — make sure to update it so NSGs will be attached to the subnets.  

2. Run the updated `task.ps1` script to create a cloud infrastructure for the web app. 

3. Run artifacts generation script `scripts/generate-artifacts.ps1`.

4. Test yourself using the script `scripts/validate-artifacts.ps1`.

5. Make sure that changes to both `task.ps1` and `result.json` are committed to the repo, and submit the solution for review. 

6. You can keep the resources if you want to — anyway, the virtual network resource itself is [free](https://azure.microsoft.com/en-us/pricing/details/virtual-network/) 

## How to complete tasks in this module 

Tasks in this module are relying on 2 PowerShell scripts: 

- `scripts/generate-artifacts.ps1` generates the task “artifacts” and uploads them to cloud storage. An “artifact” is evidence of a task completed by you. Each task will have its own script, which will gather the required artifacts. The script also adds a link to the generated artifact in the `artifacts.json` file in this repository — make sure to commit changes to this file after you run the script. 
- `scripts/validate-artifacts.ps1` validates the artifacts generated by the first script. It loads information about the task artifacts from the `artifacts.json` file.

Here is how to complete tasks in this module:

1. Clone task repository;

2. Make sure you completed the steps, described in the Prerequisites section;

3. Complete the task described in the Requirements section;

4. Run `scripts/generate-artifacts.ps1` to generate task artifacts. The script will update the file `artifacts.json` in this repo;

5. Run `scripts/validate-artifacts.ps1` to test yourself. If tests are failing — follow the recommendation from the test script error message to fix or re-deploy your infrastructure. When you are ready to test yourself again — **re-generate the artifacts** (step 4) and re-run tests again; 

6. When all tests pass — commit your changes and submit the solution for a review; 

Pro tip: if you are stuck with any of the implementation steps — run `scripts/generate-artifacts.ps1` and `scripts/validate-artifacts.ps1`. The validation script might give you a hint on what you should do.  


