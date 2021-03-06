# MEA Arc partners program for customers

MEA Arc partners program for customers is a program launched by Microsoft MEA to show the value of Microsoft hybrid cloud and Azure Arc to customers.  
the program has a specific set of activites that are delivered by qualified partners to customers.
the below is meant to be used as a delivery guidance for partners.

Disclaimer: The intention for this repo is to focus on the core Azure Arc capabilities, deployment scenarios, use-cases and ease of use. It does not focus on Azure best-practices or the other technology and OSS projects being leveraged in the guides and code.

## Azure Arc overview 

Azure Arc simplifies governance and management by delivering a consistent multi-cloud and on-premises management platform. Azure Arc enables you to manage your entire environment, with a single pane of glass, by projecting your existing resources into Azure Resource Manager. You can now manage virtual machines, Kubernetes clusters, and databases as if they are running in Azure. Regardless of where they live, you can use familiar Azure services and management capabilities. Azure Arc enables you to continue using traditional ITOps, while introducing DevOps practices to support new cloud native patterns in your environment.

Today, Azure Arc allows you to manage the following resource types hosted outside of Azure:

Servers - both physical and virtual machines running Windows or Linux.  
Kubernetes clusters - supporting multiple Kubernetes distributions.  
Azure data services - Azure SQL Database and PostgreSQL Hyperscale services.  

### Key features of Azure Arc include:

1- Implement consistent inventory, management, governance, and security for your servers across your environment.  
2- Configure Azure VM extensions to use Azure management services to monitor, secure, and update your servers.  
3- Manage and govern Kubernetes clusters at scale.  
4- Use GitOps-based configuration as code management to deploy applications and configuration across one or more clusters directly from source control, such as GitHub.  
5- Zero touch compliance and configuration for your Kubernetes clusters using Azure Policy.  
6- Run Azure data services on any Kubernetes environment, specifically Azure SQL Managed Instance and Azure Database for PostgreSQL Hyperscale, with benefits such as upgrades/updates, security, and monitoring as if it runs in Azure. Leverage elastic scale, apply updates, without any application downtime, even if it doesn't have a continuous connection to Azure.  
7- A unified experience viewing your Azure Arc enabled resources whether you are using the Azure portal, the Azure CLI, Azure PowerShell, or Azure REST API.  


## Scope of work 
partners are expected to deliver the following activities with the agreed customers  

1- Deliver Hybrid Cloud Overview ( Azure hybrid cloud overview )  - 2 hours  
2- Deliver Azure Arc Overview ( Azure Arc overview  ) - 1 hour  
3- Deliver Azure Arc Demo - 1 hour   
4- Pilot Planning Session – 1.5 hours   
5- Pilot Implementation (Arc Onboarding and use cases deployment - 5+ Servers ) 6 hours  
6- Future plans – 2 hours 

please note : estimated time is only for guidance purpose. customer requirements and priotiries comes first in time allocation

### 1- Deliver Hybird cloud overview  

The purpose of this session is to illustrate microsofy hybrid cloud strategy and vision to the customer and identify potential services that could benifit the customer. These identified services would be discussed in the future plans session at the end of the workshop . please keep the discussion interactive with the customer to identify potential azure hybrid services of interest as you would need to build a plan for deploying these services with the customer in the last day. 

please download the presentaion slide deck [here](https://arccontent.blob.core.windows.net/slides/1-Azure_Hybrid_Cloud_overview.pptx)


### 2- Deliver Azure Arc overview

The purpose of this session is to discuss in details Azure Arc Value , features , architecture and roadmap and identify specific Arc use cases that would bring value to the customer.

please download the presentaion slide deck [here](https://arccontent.blob.core.windows.net/slides/2-Azure_Arc_Overview.pptx)  
please note : hidden slides ( 78 to 84 ) under section " Partner business value" are for partners to understand the business oppourtunity for Azure Arc. they would be irrelevant in the customer discussion and should not be presented. 

### 3- Deliver Azure Arc Demo

The purpose of the demo is to deliver a hands on experience to the customer for on-boarding a server using Azure Arc.  
The demo should show an end to end scenario for onboarding a vm to azure then utilizing one of Azure Arc capabilities.  

The below deployment scenarios will guide you through onboarding various Windows and Linux server deployments to Azure with Azure Arc. 

**Note: For a list of supported operating systems and Azure regions, please visit the official [Azure Arc docs](https://docs.microsoft.com/en-us/azure/azure-arc/servers/overview).**


#### creating virtual machines and connecing to Azure Arc

The following examples can be used to connect existing Windows or Linux servers to Azure with Azure Arc. Use these if you already have existing servers that you want to project into Azure. however if you don't have any servers to use for the lab , you would need to create a server first. you will need to create a Resouce group on azure and deploy a windows and linux server in that resource group , this will mimic connecting on-premises virtual machines to azure Arc. please create either the windows and linux virtual machines before using the below links to connect the virtual machines to Azure Arc. please note that Arc currently does not support virtual machines running on azure and there is a specific script ( below ) you would need to run for you to be able to setup the Arc agent on an Azure virtual machine. it's stronly recommended to connect non Azure Virtual machines to Arc in that section.

##### creating virtual machines 
you can use the below guide to create a virtual machine on azure 

* [Creating an ubuntu linux virtual machine on azure](https://docs.microsoft.com/bs-cyrl-ba/azure/virtual-machines/linux/quick-create-portal)

* [Creating a Windows virtual machine on azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-portal)

##### connecting the virtual machines to Azure Arc


**please note: that on-boarding Azure Virtual machines to Azure ARC is not supported and you would need to run the below commands to be able to setup the arc agent before attempting to agent installation . 
If you are onboarding a Non Azure Virtual machines to Azure Arc you don't need to run the below Powershell or bash scripts and can directly deploy the agent following the documentation here * [Recommended : Connect an existing Windows and linux server to Azure Arc using scripted and manual method](https://docs.microsoft.com/en-us/azure/azure-arc/servers/onboard-portal)   

###### *Windows* powershell

```  
Write-Host "Configure the OS to allow Azure Arc Agent to be deploy on an Azure VM"  
Set-Service WindowsAzureGuestAgent -StartupType Disabled -Verbose  
Stop-Service WindowsAzureGuestAgent -Force -Verbose  
New-NetFirewallRule -Name BlockAzureIMDS -DisplayName "Block access to Azure IMDS" -Enabled True -Profile Any -Direction Outbound -Action Block -RemoteAddress 169.254.169.254 
```

###### *Linux* bash 
```
echo "Configuring walinux agent"  
sudo service walinuxagent stop  
sudo waagent -deprovision -force  
sudo rm -rf /var/lib/waagent  
echo "Configuring Firewall"  
sudo ufw --force enable  
sudo ufw deny out from any to 169.254.169.254  
sudo apt-get update  
```

The script to automate the download and installation, and to establish the connection with Azure Arc, is available from the Azure portal. To complete the process, follow the following links:

* [Recommended : Connect an existing Windows and linux server to Azure Arc using scripted and manual method](https://docs.microsoft.com/en-us/azure/azure-arc/servers/onboard-portal)

* [Optional : Connect an existing Linux server to Azure Arc - Scripted method 'Additional Reference'](azure_arc_servers_jumpstart/docs/onboard_server_linux.md)

* [Optional : Connect an existing Windows machine to Azure Arc - Scripted method 'Additional Reference'](azure_arc_servers_jumpstart/docs/onboard_server_win.md)


### 4- Pilot planning session 

the purpose of the pilot planning session is to understand the customer environment , identify selected servers to on boarded to Arc and identify specific use cases to deliver the agreed business value for customers 

the below activities should be carried out in the pilot planning session  
   1- Whiteboarding session for the customer environment  
   2- identifying the business and technical values that would benifit the customer  
   3- Selection for specific servers to be onboarded into Arc ( 5+ Servers  )  
   4- Selection for Arc (core) use cases for the projected servers incuding but not limited to
         
          Organization and inventory – Search, Index, Group, Tags  
          Environments and automation – Templates, Extensions  
          Access and security –  RBAC, Subscription  
          Azure Policy ( Basic )  
          Update Management    
          
   5- Identifying potential additional (optional) use cases for the on-boarded servers including but not limited to 
           
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
                
### 5- Pilot deployment 

the below activities should be carried out in the pilot Deployment session  
   1- Azure Arc agent deployment to the selected 5+ Servers which can be Virtual or Phyiscal machines from the supported OS list.   
   2- Verifying that the servers are projected to Azure portal.  
   3- Deployment of the specific core Azure Arc use cases indetified in the pilot planning session.    
   4- optional deployment of the specific optional use cases identified in the pilot planning session including deployment of additional         agents if required.   
   5- Demonstration of the use cases and projected servers to the customer.  
   
[Microsoft Arc offial documentation](https://docs.microsoft.com/en-us/azure/azure-arc/) should be used as deployment guide for the agreed specific use cases, however you can also utilize the [Azure Arc jumpstart](https://github.com/microsoft/azure_arc) . The jumpstart does not focus on deployment best practices but rather provide a guide into building a demo environment for different use cases. It provides a walk through the process of setting up demos that show how to get started with Azure Arc. They are designed with a "zero to hero" approach in mind and with as much automation as possible. The goal of the jumpstart is to provide a working Azure Arc demo nvironment spun up in no time so you can focus on showing the core values of the solution.



### 6- Future Plans

the below activities should be carried out in the Advanced Azure Arc plan  

   1- Identifying  potential additional sites or servers for Arc deployment.  
   2- Identifying  potential additional use cases and plans including but not limited to      
           
            Azure Arc enabled Data services
            Azure Arc enabled kubernetes 
            Azure Arc enabled servers additional usecases   
            Azure Monitor  
            Security Center  
            Azure Sentinel  
            Backup  
            Log Analytics  
            Service Map  
            Application Insights  
            Network Watcher    
            Config and Change Management   
                     
   3- lisitng potential additional Azure hybrid services for the customer identified from the "Hybrid cloud overview" session  
   4- agreeding on timelines and plan to deliver the agreed identified solutions   
   


