# Azure Arc overview 

Today, companies are struggling to control and govern an environment that becomes more and more complex. These environments extend across data centers, multiple clouds, and edge. Each environment and cloud have its own set of disjointed management tools that you need to learn and operate.

In parallel, new DevOps and ITOps operational models are hard to implement, as existing tools fail to provide support for new cloud native patterns.

Azure Arc simplifies governance and management by delivering a consistent multi-cloud and on-premises management platform. Azure Arc enables you to manage your entire environment, with a single pane of glass, by projecting your existing resources into Azure Resource Manager. You can now manage virtual machines, Kubernetes clusters, and databases as if they are running in Azure. Regardless of where they live, you can use familiar Azure services and management capabilities. Azure Arc enables you to continue using traditional ITOps, while introducing DevOps practices to support new cloud native patterns in your environment.

Today, Azure Arc allows you to manage the following resource types hosted outside of Azure:

Servers - both physical and virtual machines running Windows or Linux.
Kubernetes clusters - supporting multiple Kubernetes distributions.
Azure data services - Azure SQL Database and PostgreSQL Hyperscale services.

Key features of Azure Arc include:

Implement consistent inventory, management, governance, and security for your servers across your environment.

Configure Azure VM extensions to use Azure management services to monitor, secure, and update your servers.

Manage and govern Kubernetes clusters at scale.

Use GitOps-based configuration as code management to deploy applications and configuration across one or more clusters directly from source control, such as GitHub.

Zero touch compliance and configuration for your Kubernetes clusters using Azure Policy.

Run Azure data services on any Kubernetes environment, specifically Azure SQL Managed Instance and Azure Database for PostgreSQL Hyperscale, with benefits such as upgrades/updates, security, and monitoring as if it runs in Azure. Leverage elastic scale, apply updates, without any application downtime, even if it doesn't have a continuous connection to Azure.

A unified experience viewing your Azure Arc enabled resources whether you are using the Azure portal, the Azure CLI, Azure PowerShell, or Azure REST API.



# MEA Arc Partners program for customers 

MEA Arc partners program for customers is a program launched by Microsoft MEA to show the value of Azure Arc to customers.  
the program has a specific set of activites that are delivered by qualified partners to customers.
the below is meant to be used as a delivery guidance for partners.    

# Scope of work 
partner is expected to deliver the following activities with the agreed customers  

please note : estimated time is only for guidance purposes 

   1- Deliver Hybrid Cloud Overview ( 1- Azure hybrid cloud overview )  - 120 mins\
   2- Deliver Azure Arc Overview ( 2 – Azure Arc overview  ) - 60 mins\
   3- Deliver Azure Arc Demo - 60 mins\
   4- Pilot Planning Session – 90 mins\
   5- Pilot Implementation (Arc Onboarding - 10-20 VMs) 12 hours  
   6- Advanced Azure Arc Plan – 120 mins\

## Deliver Azure Arc Demo

the purpose of the demo is to deliver a hands on experience to the customer for on-boarding a server using Azure Arc

The below deployment scenarios will guide you through onboarding various Windows and Linux server deployments to Azure with Azure Arc. 

**Note: For a list of supported operating systems and Azure regions, please visit the official [Azure Arc docs](https://docs.microsoft.com/en-us/azure/azure-arc/servers/overview).**


#### Step 1 - creating virtual machines and connecing to Azure Arc

The following examples can be used to connect existing Windows or Linux servers to Azure with Azure Arc. Use these if you already have existing servers that you want to project into Azure. however if you don't have servers to use for the lab , you would need to create them first. as a prerequiste you will need to create a Resouce group on azure and deploy a windows and linux server in that resource group , this will mimic connecting on-premises virtual machines to azure Arc. please create both the windows and linux virtual machines before using the below links to connect the virtual machines to Azure Arc. please note that Arc currently does not support virtual machines running on azure and there is a specific script ( below ) you would need to run for you to be able to setup the Arc agent on an Azure virtual machine.

##### creating virtual machines 
you can use the below guide to create a virtual machine on azure 

* [Creating an ubuntu linux virtual machine on azure](https://docs.microsoft.com/bs-cyrl-ba/azure/virtual-machines/linux/quick-create-portal)

* [Creating a Windows virtual machine on azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-portal)

##### connecting the virtual machines to Azure Arc


**please note: that on-boarding Azure Virtual machines to Azure ARC is not supported and you would need to run the below commands to be able to setup the arc agent before attempting to setup the agent 

##### *Windows* powershell

Write-Host "Configure the OS to allow Azure Arc Agent to be deploy on an Azure VM"  
Set-Service WindowsAzureGuestAgent -StartupType Disabled -Verbose  
Stop-Service WindowsAzureGuestAgent -Force -Verbose  
New-NetFirewallRule -Name BlockAzureIMDS -DisplayName "Block access to Azure IMDS" -Enabled True -Profile Any -Direction Outbound -Action Block -RemoteAddress 169.254.169.254   

##### *Linux* bash 

echo "Configuring walinux agent"  
sudo service walinuxagent stop  
sudo waagent -deprovision -force  
sudo rm -rf /var/lib/waagent  
echo "Configuring Firewall"  
sudo ufw --force enable  
sudo ufw deny out from any to 169.254.169.254  
sudo apt-get update  
echo "Reconfiguring Hostname"  
sudo hostname $VMNAME  
sudo -E /bin/sh -c 'echo $VMNAME > /etc/hostname'  

The script to automate the download and installation, and to establish the connection with Azure Arc, is available from the Azure portal. To complete the process, follow the following links:

* [Recommended : Connect an existing Windows and linux server to Azure Arc using scripted and manual method](https://docs.microsoft.com/en-us/azure/azure-arc/servers/onboard-portal)

* [Optional : Connect an existing Linux server to Azure Arc - Scripted method 'Additional Reference'](azure_arc_servers_jumpstart/docs/onboard_server_linux.md)

* [Optional : Connect an existing Windows machine to Azure Arc - Scripted method 'Additional Reference'](azure_arc_servers_jumpstart/docs/onboard_server_win.md)


## Pilot planning session 

the purpose of the pilot planning session is to understand the customer environment , identify selected servers to on boarded to Arc and identify specific use cases to deliver the identified business value for customers 

the below activities should be carried out in the pilot planning session 
   1- Whiteboarding session for the customer environment  
   2- identifying the business and technical value that would benifit the customer  
   3- Selection for specific servers to be onboarded into Arc ( 10-20 )  
   4- Selection for Arc use cases for the projected servers incuding but not limited to 
         Organization and inventory – Search, Index, Group, Tags
         Environments and automation – Templates, Extensions
         Access and security –  RBAC, Subscription
         Azure Policy ( Basic )
         Update Management
    
## Pilot deployment 

the below activities should be carried out in the pilot Deployment session   
   1- Azure Arc agent deployment into the selected 10-20 VMs  
   2- Verifying that the servers are projected to Azure portal  
   3- Applying the specific agreed use cases in the pilot planning session  
   4- Demonstrating the use cases and projected servers to the customer   

## Advanced Azure Arc Plan

the below activities should be carried out in the Advanced Azure Arc plan  
   1- Identifying  potential additional sites/servers , use cases and plans for Arc including but not limited to   
            Azure Policy ( advanced )  
            Azure Monitor  
            Security Center  
            Azure Sentinel  
            Backup  
            Log Analytics  
            Service Map  
            Application Insights  
            Network Watcher    
            Config and Change Management   
   2- identifying potential additional Azure hybrid services for the customer   
   3- agreeding on timelines and plan to deliver the agreed activities  
   


