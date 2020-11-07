# MEAArc


# Scope of work 
partner to deliver with identified customer to deliver the following activities 
estimated time is only for guidance purposes 

  Deliver Hybrid Cloud Overview ( 1- Azure hybrid cloud overview )  - 120 mins
  Deliver Azure Arc Overview ( 2 – Azure Arc overview  ) - 60 mins 
  Deliver Azure Arc Demo - 60 mins 
  Pilot Planning Session – 90 mins 
  Pilot Implementation (Arc Onboarding - 10-20 VMs) 12 hours 
  Advanced Azure Arc Plan – 120 mins 

## DEMO - Azure Arc enabled Servers

the purpose of the demo is to deliver a hands on experience to the customer for on-boarding a server using Azure Arc

The below deployment scenarios will guide you through onboarding various Windows and Linux server deployments to Azure with Azure Arc. 

**Note: For a list of supported operating systems and Azure regions, please visit the official [Azure Arc docs](https://docs.microsoft.com/en-us/azure/azure-arc/servers/overview).**


#### Step 1 - creating virtual machines and connecing to Azure Arc

The following examples can be used to connect existing Windows or Linux servers to Azure with Azure Arc. Use these if you already have existing servers that you want to project into Azure. however if you don't have servers to use for the lab , you would need to create them first. as a prerequiste you will need to create a Resouce group on azure and deploy a windows and linux server in that resource group , this will mimic connecting on-premises virtual machines to azure Arc. please create both the windows and linux virtual machines before using the below links to connect the virtual machines to Azure Arc . 

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

the purpose of the pilot planning session is to understand the customer environment , identify selected servers to on boarded to Arc and identify specific use cases to deliver the business value for customers 

  White boarding session for customer environment
  Selection for specific servers to be onboarded into Arc ( 10-20 )
  Selection for use cases for Arc for the projected servers  
    Organization and inventory – Search, Index, Group, Tags
    Environments and automation – Templates, Extensions
    Access and security –  RBAC, Subscription
    Azure Policy ( Basic )
    Update Management
    
## Pilot deployment 

Azure Arc agent deployment into the selected 10-20 VMs
Verifying that the servers are projected to Azure portal
Applying the specific agreed use cases in the pilot planning session
Demonstrating the use cases and projected servers to the customer 


## Advanced Azure Arc Plan


Identifying  potential additional use cases and plans for Arc including 
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

