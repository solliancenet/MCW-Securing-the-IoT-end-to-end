![](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
Securing the IoT end to end
</div>

<div class="MCWHeader2">
Hands-on lab step-by-step
</div>

<div class="MCWHeader3">
June 2019
</div>


Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2019 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents** 

<!-- TOC -->

- [Securing the IoT End to End hands-on lab step-by-step](#\insert-workshop-name-here\-hands-on-lab-step-by-step)
    - [Abstract and learning objectives](#abstract-and-learning-objectives)
    - [Overview](#overview)
    - [Solution architecture](#solution-architecture)
    - [Requirements](#requirements)
    - [Before the hands-on lab](#before-the-hands-on-lab)
    - [Exercise 1: Secure and Configure IoT Hub and Device Provisioning Service](#exercise-1-secure-and-configure-iot-hub-and-device-provisioning-service)
        - [Task 1: Link Provision Service to IoT Hub](#task-1-link-device-provisioning-service-to-iot-hub)
        - [Task 2: Enable Azure Security Center for IoT](#task-2-enable-azure-security-center-for-iot)
        - [Task 3: Configure Diagnostic Logging on IoT Hub](#task-3-configure-diagnostic-logging-on-iot-hub)
        - [Task 4: Configure Diagnostic Logging on Device Provisioning Service](#task-4-configure-diagnostic-logging-on-device-provisioning-service)
    - [Exercise 2: Enroll and Provision IoT Devices](#exercise-2-enroll-and-provision-iot-devices)
        - [Task 1: Configure your devcies](#task-1-configure-your-devices)
        - [Task 2: Update and Install Azure IoT SDK prerequisites](#task-2-update-and-install-azure-iot-sdk-prerequisites)
        - [Task 3: Download and compile the Azure IoT SDK](#task-3-download-and-compile-the-azure-iot-skd)
        - [Task 4: Attempt Device Enrollment](#task-4-attempt-device-enrollment)
        - [Task 5: Install a software TPM and Resource Manager](#task-5-install-a-software-tpm-and-resource-manager)
    - [Exercise 3: Install and Configure IoT Edge](#exercise-3-install-and-configure-iot-edge)
        - [Task 1: Install IoT Edge](#task-1-install-iot-edge)
        - [Task 2: Configure the IoT Edge Agent](#task-2-configure-the-iot-edge-agent)
    - [Exercise 4: Install Azure Security IoT Agent](#exercise-4-install-azure-security-iot-agent)
        - [Task 1: Install the Security Agent](#task-1-install-the-security-agent)
        - [Task 2: Install the IoT Hub Security Agent Module](#task-2-install-the-iot-hub-security-agent-module)
    - [Exercise 5: Simulate IoT Attacks](#exercise-5-simulate-iot-attacks)
        - [Task 1: Setup and execute Attack Scripts](#task-1-setup-and-execute-attack-scripts)
    - [Exercise 6: Configure Security and Alerts](#exercise-6-configure-security-and-alerts)
        - [Task 1: Review Security Log Data](#task-1-review-security-log-data)
        - [Task 2: Create Custom Security Alerts for Device Events](#task-2-create-custom-security-alerts-for-device-events)
        - [Task 3: Create Custom Security Alerts for Azure Events](#task-3-create-custom-security-alerts-for-azure-events)
    - [After the hands-on lab](#after-the-hands-on-lab)
        - [Task 1: Delete resource group](#task-1-delete-resource-group)

<!-- /TOC -->

# Securing the IoT End to End hands-on lab step-by-step 

## Abstract and learning objectives 

In this hands-on-lab, you will implement an IoT solution that utilizes the latest Azure Security IoT features.  Specifically you will provision a set of Azure resources that will securly manage your IoT infrastructure and devices.  This includes provisioning Azure IoT Edge devices with supporting modules and agents.

Once deployed and configured, you will simulate various events from the devices that will then generate specific alerts in the Azure Security Center for IoT.  You can then use these alerts to diagnosis issues with your devices and execute commands to remediate those issues.

At the end of this lab you will have a better understanding of how the latest Azure Security features work with IoT environments as well as how to install, configure and troubleshoot issues.

## Overview

Contoso, Ltd. has major holdings in one of the world’s most important oil-producing regions. To overcome the challenges of monitoring and optimizing a vast number of widely dispersed field assets, Contoso, Ltd. is looking to streamline its operations with IoT solutions. They want to deploy IoT technologies to electronically collect data and use cloud based solutions to store and analyze it in order to gain new insights into well operations and future drilling possibilities. 

Their environments are very tough environments in which to work. The climate is hot, harsh, and unforgiving, and oil wells are often spaced many miles apart, so field technicians can spend much of their day just driving from one to another. Cellular and radio reception is spotty at best, so collecting data about well conditions and performance typically involves manually writing down information. The technician must then make the long trek to the central office at the end of the day to upload the data for analysis. With such remote situations, a key concern for Contoso is not only how they manage these remote devices, but more broadly how they secure the complete solution that encompasses the physical device, the software on the device, the services processing the data in the cloud and the network connecting it all. 

Contoso plans to tie in to existing sensors at the well head that monitor key system parameters like temperatures, pressures, and flow rates. They will deploy gateway devices to route device data for processing, storage and analytics. Internal IT staff and engineers want to visualize the high-resolution data and deliver near real-time analyses. The company is placing a premium on flexibility and ease of use, with security as a fundamental driver. 

In addition, they would also like the solution to yield benefits to their workers in the field. “The field technicians and lease operators already have tools on their phones that they use every day to see what a well is doing,” explains Miles Strom. “Our goal is to connect these tools to live data from the IoT sensors. So, instead of seeing low-resolution volumes or flow rates, they’ll see what is happening in real time. This way they can respond immediately to problems that lead to downtime or maintenance issues.”

They have implemented a proof of concept solution for collecting and analyzing device telemetry using IoT Hub, but are interested in learning about any related services in Azure that would help them to secure such solutions.

## Solution architecture (High-level)

![The proposed solution utilizing Azure Security Center for IoT and its agents to monitor and secure the IoT Devcies.  Log data is forwarded to Log Analytics where alerts and logic apps will execute to start investigation and remediation](../Media/solution-diagram-1.png "Solution Architecture")

## Solution architecture (Analytics)

![The Analytics solution using Stream Analytics, Cosmos DB, Time-series and a hosted application in an App Server](../Media/solution-diagram-2.png "Analytics Solution")

## Requirements

1. Microsoft Azure subscription must be pay-as-you-go or MSDN.

    - Trial subscriptions will not work.
    
## Before the hands-on lab

Refer to the Before the hands-on lab setup guide manual before continuing to the lab exercises.

## Exercise 1: Secure and Configure IoT Hub and Device Provisioning Service

Duration: 15 minutes

Synopsis:  In this exercise you will link your provisioning service to your IoT Hub.  Once this is completed, you will enable the Azure Security Center for IoT on your IoT Hub.  With this plumbing in place, you can start to create your device enrollments and to provision your IoT devices. 

You will also enable diagnostic logging such that you can create custom alerts later in this lab.

### Task 1: Link Device Provisioning Service to IoT Hub

1.  Open the Azure Portal

2.  Select the **oilwells-prov-[YOUR INITS]** resource

3.  In the Device Provisioning Service blade, under **Settings**, select **Linked IoT Hubs**

4.  Click **Add**

![Linked IoT Hubs](Images/Hands-onlabstep-bystep-securitytheiotendtoendimages/media/ex1_image001.png "Linked IoT Hubs")

5.  Select the **oilwells-iothub-[YOUR INITS]** IoT hub

6.  Select the **iotowner** access policy

![Adding an IoT Hub link](Images/Hands-onlabstep-bystep-securitytheiotendtoendimages/media/ex1_image002.png "Linked IoT Hubs")

7.  Click **Save**

### Task 2: Enable Azure Security Center for IoT

1.  Navigate to your resource group 

2.  In the menu, select the **oilwells-iothub-[YOUR INITS]** IoT Hub

3.  In the resource blade, scroll down to the **Security** section and click **Overview**

4.  In the overview area, click **Start preview**

5.  In the settings, click **Enable**

6.  For the workspace, select **oilwells-logging-[YOUR INIT]**

![Enabling the Azure Security Center for IoT](Images/Hands-onlabstep-bystep-securitytheiotendtoendimages/media/ex1_image004.png "Enable Security Center settings")

7.  Click **Save**

### Task 3: Configure Diagnostic Logging on IoT Hub

1.  Open your Azure Portal

2.  Click the **oilwells-iothub-[YOUR INIT]** IoT hub

3.  In the blade menu, scroll to the **Monitoring** section, then click **Diagnostic settings**

4.  Click **Add diagnostic setting**

5.  For the name, type **oilwells-iothub-logging**

6.  Check the **Send to Log Analtyics** checkbox, and then select the **oilwells-logging-[YOUR INIT]** workspace

7.  Check all the LOG checkboxes

8.  Click **Save**

### Task 4: Configure Diagnostic Logging on Device Provisioning Service

2.  Click the **oilwells-prov-[YOUR INIT]** IoT Device Provisioning Service

3.  In the blade menu, scroll to the **Monitoring** section, then click **Diagnostic settings**

4.  Click **Add diagnostic setting**

5.  For the name, type **oilwells-prov-logging**

6.  Check the **Send to Log Analtyics** checkbox, and then select the **oilwells-logging-[YOUR INIT]** workspace

7.  Check all the LOG checkboxes

8.  Click **Save**

> NOTE:  It may take 5-10 minutes for event data to populate into the Log Analytics and then for Security Center recommendations to display

## Exercise 2: Enroll and Provision IoT Devices

Duration: 30 minutes

Synopsis: With the Azure resources in place, you can now start creating and provisioning devices into your Azure IoT hub.  Here you will create several devices and configure them with the Azure IoT SDK, agents and modules to allow you to provision and utilize the security services offered by Azure.

### Task 1: Configure your devices

1.  Navigate to your Azure Resource Group

2.  Select the **oilwells-edgevm-cjg**

3.  Click **Connect**

![Click Connect](Images/Hands-onlabstep-bystep-securitytheiotendtoendimages/media/ex2_image001.png "Enable Security Center settings")

4.  Open a Windows Powershell window, execute the following and copy the SSH details into the window.

5.  When prompted, type **yes** then press **ENTER**

6.  Copy the SSH details, press **ENTER**

7.  When prompetd, enter the password **S2@dmins2@dmin**.  You should now be logged into the device.

![SSH Session Login](Images/Hands-onlabstep-bystep-securitytheiotendtoendimages/media/ex2_image002.png "Enable Security Center settings")

### Task 2: Update and install Azure IoT SDK prerequisites

1.  Run the following commands, this could take up to 10 minutes to complete:

```PowerShell
sudo apt-get update
sudo apt-get upgrade

sudo apt-get install -y git cmake libcurl4 build-essential curl libcurl4-openssl-dev libssl-dev uuid-dev

sudo apt-get install libcurl3 libcurl-openssl1.0-dev
sudo apt-get install auditd audispd-plugins

reboot

```

### Task 3: Download and compile the Azure IoT SDK

1.  Run the following commands

```PowerShell
git clone https://github.com/Azure/iotedge --recursive

git clone -b 2019-05-16 https://github.com/Azure/azure-iot-sdk-c.git --recursive

cd azure-iot-sdk-c

git submodule update --init
```

If you are using a software based simulator, then run the following command:

```PowerShell

cmake -Duse_prov_client:BOOL=ON -Duse_tpm_simulator:BOOL=OFF .

Otherwise with a hardware based TPM, run the following:

```PowerShell
cmake -Duse_prov_client:BOOL=ON -Duse_tpm_simulator:BOOL=OFF .
```

To get a new registration and endoresment key, run the following:

```PowerShell
cd provisioning_client/tools/tpm_device_provision

make
```

### Task 4: Attempt Device Enrollment 

1.  Run the following commands:

```PowerShell
sudo ./tpm_device_provision
```

>NOTE:  This command will fail on a device that does not have a hardward or software TPM installed.  In order to utilize a hardward based TPM, you would need an actual device, or a nested TPM enabled virtual machine running.  The Azure template provisionged an Ubuntu image that does not have a hardward TPM enabled.

![This shows what happens with the device does not have a hardware or software TPM ](Images/Hands-onlabstep-bystep-securitytheiotendtoendimages/media/ex2_image003.png "Failed TPM command")

### Task 5: Install a software TPM and Resource Manager and reattempt Device Enrollment

> NOTE:  If you have a hardware TPM in your device, you can skip to step 3

1.  Run the following commands to download, compile and start a software based TPM server

```PowerShell
cd

sudo wget -c https://cfhcable.dl.sourceforge.net/project/ibmswtpm2/ibmtpm1332.tar.gz

sudo tar -zxvf ibmtpm1332.tar.gz 

cd src
sudo make

./tpm_server &
```

![A running software TPM.](Images/Hands-onlabstep-bystep-securitytheiotendtoendimages/media/ex2_image004.png "A running software TPM")

2.  Run the following commands to start a TPM resource manager:

```PowerShell

cd 

sudo apt-get install autoconf
sudo apt-get install libtool
sudo apt-get install pkg-config

sudo wget -c https://astuteinternet.dl.sourceforge.net/project/ibmtpm20tss/ibmtss1470.tar.gz

sudo tar -zxvf ibmtss1470.tar.gz 

autoreconf -i
./configure --prefix=${HOME}/local --disable-hwtpm
make
make install

cd local/bin
./tsspowerup &
./tssstartup &

```

3.  With your software TPM running, attempt to provision again using the following commands:

```PowerShell
cd
cd azure-iot-sdk-c/provisioning_client/tools/tpm_device_provision
sudo ./tpm_device_provision
```

![A running software TPM.](Images/Hands-onlabstep-bystep-securitytheiotendtoendimages/media/ex2_image005.png "A running software TPM")


4.  Copy the device **Registration Id** and the **Endorsement Key**

> NOTE: In the real world all your devices should have hardware based TPMs.

5.  Switch to the Azure Portal and navigate to the Device Provisioning Service **oilwells-prov-[YOUR INIT]**

6.  Under **Settings**, click **Manage enrollments**

7.  Click **Add Individual Enrollment**

8.  Enter your Registration Id and Endorsement Key, then click the **Enable** toggle for the IoT Edge Device setting

9.  Click **Save**

## Exercise 3: Install and Configure IoT Edge

Duration: 30 minutes

In this exercise you will install the Azure IoT Edge agent on your IoT device and then register the new device with your IoT Hub.

### Task 1: Install IoT Edge

1.  Run the following command:

>NOTE: Change the ubuntu version as appropriate (16.04 vs 18.04).  You can get your version by running "lsb_release -a"

```PowerShell
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list

sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/

curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg

sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/

sudo apt-get update

sudo apt-get install moby-engine
sudo apt-get install moby-cli

sudo apt-get install iotedge
```

### Task 2: Configure the IoT Edge Agent

1.  Switch to the Azure Portal, open your **oilwells-prov-[YOUR INIT]** device provisioning resource

2.  In the overview, copy the **ID Scope**

3.  Open the **oilwells-iothub-[YOUR INIT]** IoT Hub.  

4.  Under **Automatic Device Management**, click **IoT Edge**

5.  Click **Add IoT Edge Device**

6.  For the Device Id, type **OilWells001**

7.  Click **Save**, then select the new **OilWells001** item

8.  Copy the primary device connection string

9.  Run the following command to open a text editor:

```PowerShell
sudo nano /etc/iotedge/config.yaml
```

10.  There are several ways to register your device with the provisioning service.  This includes "manual" with a device connection string, TPM registration, and symmetric key.  The most simple provisioning method is "manual" with a device connection string.  Each way is presented below, you need only pick one.  Note that TPM registration requires a software or hardware TPM:

> NOTE:  Be sure that the leading lines have "tabs" that are made up of only 2 space characters.

-  Manual Provisioning

    -  Copy the device connection string from the IoT Hub, paste it into the config.yaml file
    -  Save the file

-  Symmetric Key Provisioning

    -  Comment out the manual provision settings, uncomment the **dps symmetric key** settings, then copy in the symmetric key and Registration Id information
    -  Save the file

-  TPM Provisioning

    -  Comment out the manual provision settings, uncomment the **dps TPM** settings, then copy in the Id Scope and Registration Id information:

    ![A running software TPM.](Images/Hands-onlabstep-bystep-securitytheiotendtoendimages/media/ex2_image008.png "A running software TPM")

    -  Although we are using a software TPM, you would need to give permissions to the hardware TPM to the iotedge service by running the following commands:

```PowerShell
tpm=$(sudo find /sys -name dev -print | fgrep tpm | sed 's/.\{4\}$//')

sudo touch /etc/udev/rules.d/tpmaccess.rules
```

    -  Run the following command to open a text editor:

```PowerShell
sudo nano /etc/udev/rules.d/tpmaccess.rules
```

    -  Copy the following into the file:

```PowerShell
# allow iotedge access to tpm0
KERNEL=="tpm0", SUBSYSTEM=="tpm", GROUP="iotedge", MODE="0660"
```
    -  Execute the following:

```PowerShell
/bin/udevadm trigger $tpm
```

11.  Run the following commands to restart the iotedge service:

```PowerShell
sudo systemctl restart iotedge
sudo systemctl status iotedge
```

12.  You should see the status as **active**.  

![The Azure IoT Edge daemon shows active.](Images/Hands-onlabstep-bystep-securitytheiotendtoendimages/media/ex2_image009.png "Successful service start")

> NOTE: If you do not, then run the following command to see diagnostics logs that may help you troubleshoot the issue: 

```PowerShell
sudo journalctl -u iotedge
```

14.  The IoT Edge modules will be downloaded and created in docker containers, you can review the docker images by running:

```PowerShell
sudo docker ps
```

## Exercise 4: Install Azure Security IoT Agent

Duration: 15 minutes

In this exercise you will install the Azure Security IoT Agent directly and via an Azure IoT Edge module.

### Task 1: Install the Security Agent

1.  Run the following command:

```PowerShell
cd

git clone https://github.com/Azure/Azure-IoT-Security-Agent-C.git --recursive

sudo apt-get install libcurl3 libcurl-openssl1.0-dev
sudo apt-get install auditd audispd-plugins

#extract the release binaries

cd Azure-IoT-Security-Agent-C/release

sudo tar -zxvf ubuntu-16.04-x64.tar.gz
sudo cp -r agent/Install/. /var/ASCIoTAgent

cd /var/ASCIoTAgent

sudo chmod +x InstallSecurityAgent.sh

sudo ./InstallSecurityAgent.sh -aui Device -aum SymmetricKey -f /var/certs/key -hn oilwells-iothub-[YOURINIT].azure-devices.net -di OilWell001 -i

sudo mkdir /var/certs

sudo nano /var/certs/key
```
2.  Copy the primay key for the device from the Azure Portal and copy it into the file

3.  Run the following command to start the security agent:

```PowerShell
sudo systemctl start ASCIoTAgent
sudo systemctl status ASCIoTAgent
```

4.  The status of the service will not be **started**.  Run the following command:

```PowerShell
sudo journalctl -u ASCIoTAgent
```

5.  You should see an error about the azureiotsecurity module not being registered

TODO

### Task 2: Install the IoT Hub Security Agent Module

1.  Switch to the Azure Portal

2.  Open the **oilwells-iothub-[YOUR INIT]** IoT Hub

3.  Click **IoT Edge**

4.  Select the device

5.  Click **Set Modules**

6.  Click **Add**, then select **IoT Edge Module**

7.  For the name, type **azureiotsecurity**

8.  For the Image URI, type:

```
mcr.microsoft.com/ascforiot/azureiotsecurity:0.0.3
```

9.  In the Container Create Options, copy the following:

```
{
    "NetworkingConfig": {
        "EndpointsConfig": {
            "host": {}
        }
    },
    "HostConfig": {
        "Privileged": true,
        "NetworkMode": "host",
        "PidMode": "host",
        "Binds": [
            "/:/host"
        ]
    }
}    
```

10.  Select the **Set module twin's desired properties** checkbox

11.  Copy the following into the twin's desired properties textarea:

```
{
  "properties.desired": {
    "azureiot*com^securityAgentConfiguration^1*0*0": {
    }
  }
}
```

12.  Click **Save**

13.  Click **Configure advanced Edge Runtime settings**

14.  Change the image name to **mcr.microsoft.com/ascforiot/edgehub:1.0.9-preview**, then click **Save**

15.  Click **Next**

16.  On the routes dialog, replace with the following:

```
{
  "routes": {
    "route": "FROM /messages/* INTO $upstream",
    "ASCForIoTToIoTHub" : "FROM /messages/modules/azureiotsecurity/* INTO $upstream"
  }
}
```

17.  Click **Next**

18.  Click **Submit**

19.  Run the following command to start the security agent:

```PowerShell
sudo systemctl start ASCIoTAgent
sudo systemctl status ASCIoTAgent
```

20.  The status should now show **active**

## Exercise 5: Simulate IoT Attacks

Duration: 10 minutes

This exercise will have you install some "fake" processes and open some non-standard ports on your IoT device.  Once your attacks have been executed, the Security Agent will pick up these bad configurations and send them to the IoT Hub and the Azure Security Center will notify you.

### Task 1: Setup and Execute Attack scripts

1.  Run the following command:

```PowerShell
sudo apt-get install netcat
```

2.  Download and execute the attack script:

```PowerShell
cd

git clone https://github.com/Azure/Azure-IoT-Security --recursive

cd Azure-IoT-Security/trigger_events

sudo chmod +x trigger_events.sh

sudo ./trigger_events.sh --exploit

sudo ./trigger_events.sh --malicious
```

## Exercise 6: Configure Security and Alerts

Duration: 20 minutes

This exercise will evaluate the logs from when you enabled diagnostic logging on your Azure resources and then setup some alerts based on any important configuration changes that an Azure user may make to your IoT infrastructure.

### Task 1: Review Azure Security for IoT Log Data

1.  Open your Azure Portal

2.  Click the **oilwells-iothub-[YOUR INIT]** IoT hub

3.  In the blade menu, in the **Security** section, click **Overview**, you will get a dashboard of potential security recommendations that very likey should be implemented.

4.  Click **Recommendations**, you should see our attack items displaying:

5.  Click the **Open Ports On Device** recommendation.  In the dialog, click the **To see which devices have this recommendation...** link.  This will navigate to the Log Analytics portal when you can drill deeper into the log data that caused the alert.

6.  Expand the log

### Task 2: Create Custom Security Alerts for Device Events

1.  Open your Azure Portal

2.  Click the **oilwells-iothub-[YOUR INIT]** IoT hub

3.  In the blade menu, in the **Security** section, click **Custom Alerts**

4.  Select the **default** security group

5.  Click **Add a custom alert**

6.  Review the available options, then select **Number of failed local logins is not in allowed range**

7.  Click **Ok**, then click **Save**

### Task 3: Create Custom Security Alerts for Azure Events

1.  Open your Azure Portal

2.  Click the **oilwells-logging-[YOUR INIT]** IoT hub

3.  In the blade menu, in the **General** section, click **Logs**

4.  In the query window, paste the following:

```SQL
AzureDiagnostics
| limit 50
| where parse_json(properties_s).deviceId == "OilWells001" 
```

5.  Click **Run**, you should see all the evenst tied to that device

6.  Click **New alert rule**

7.  Select the condition, for the threshold, type **1**, click **Save**

8.  Under **Actions**, click **Add**

9.  Click **Create action group**

10.  For the group name type **Email IoT Admins**

11.  For the short name type **Email**

12.  For the action name, type **Email IoT Admins**

13.  Type an email alias

14.  Click **OK**

15.  Click **OK**

16.  For the **Alert rule name**, type **Device key reset**

17.  Click **Create alert rule**

## After the hands-on lab 

Duration: 10 minutes

In this exercise, attendees will deprovision any Azure resources that were created in support of the lab.

### Task 1: Delete resource group

1.  Using the Azure portal, navigate to the Resource group you used throughout this hands-on lab by selecting **Resource groups** in the menu.

2.  Search for the name of your research group, and select it from the list.

3.  Select **Delete** in the command bar, and confirm the deletion by re-typing the Resource group name and selecting **Delete**.

You should follow all steps provided *after* attending the Hands-on lab.

