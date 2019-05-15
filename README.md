# Securing the IoT end-to-end
Contoso, Ltd. has major holdings in one of the world’s most important oil-producing regions. To overcome the challenges of monitoring and optimizing a vast number of widely dispersed field assets, Contoso, Ltd. is looking to streamline its operations with IoT solutions. They want to deploy IoT technologies to electronically collect data and use cloud based solutions to store and analyze it in order to gain new insights into well operations and future drilling possibilities. 

Their environments are very tough environments in which to work. The climate is hot, harsh, and unforgiving, and oil wells are often spaced many miles apart, so field technicians can spend much of their day just driving from one to another. Cellular and radio reception is spotty at best, so collecting data about well conditions and performance typically involves manually writing down information. The technician must then make the long trek to the central office at the end of the day to upload the data for analysis. With such remote situations, a key concern for Contoso is not only how they manage these remote devices, but more broadly how they secure the complete solution that encompasses the physical device, the software on the device, the services processing the data in the cloud and the network connecting it all. 

Contoso plans to tie in to existing sensors at the well head that monitor key system parameters like temperatures, pressures, and flow rates. They will deploy gateway devices route device data for processing, storage and anlytics. Internal IT staff and engineers want to visualize the high-resolution data and deliver near real-time analyses. The company is places a premium on flexibility and ease of use, with security as a fundamental. 

In addition, they would also like to the solution to yield benefits to their workers in the field. “The field technicians and lease operators already have tools on their phones that they use every day to see what a well is doing,” explains Miles Strom. “Our goal is to connect these tools to live data from the IoT sensors. So, instead of seeing low-resolution volumes or flow rates, they’ll see what is happening in real time. This way they can respond immediately to problems that lead to downtime or maintenance issues.”

## Target audience
-	IoT Developers
-	Network Security Administrators
-	Network Engineers

## Abstract

### Workshop
In this workshop, you will look at the process for designing and implementating an oil and gas manufacturing IoT solution that is secured end-to-end following best practices. 

At the end of this workshop, you will be better able to architect a comprehensive and secure oil and gas manufacturing IoT solution.

![Envisioned situation](Media/envisioned-situation.png)

### Whiteboard design session
In this whiteboard design session, you will look at the process for designing a oil and gas manufacturing IoT solution that is secured end-to-end following best practices. You will learn how to apply appropriate role-based access control permission to objects in this solution such as devices, sensors, cloud services and people. You will consider how to secure the network connecting all the devices, and how to monitor them using a SIEM. You will also work through zone assignments so that you have a clear picture of device security, gateway security, cloud services security. You will also provide Contoso guidance on defining lifecycles for particular components so that they have a plan that begins with initial deployment, to expected maintenance, to planned obsolesence and ultimately thru decommissioning of the device so that they can understand how Azure supports this. Additionally, you will perform some threat modeling to help WWI think about how they might handle: denial of service attacks, tampering, elevation of privelege, intrusion, information disclosure, man in the middle and protocol attacks against devices.  

At the end of this whiteboard design session, you will be better able to architect a comprehensive and secure oil and gas manufacturing IoT solution.

#### Outline: Key Concerns for Cutomer situation ####
- What SIEM tools can we use with an IoT solution?
- How can we provide a secure identity to each of our devices?
- How can we proactively guard against attacks to components in our solution, from device, to network to cloud?
- How do we manage the lifecycle of the solution, encompassing the both the applications running on or near the device and in the cloud?
  
### Hands-on lab 
In this hands-on lab, you will look at the process for implementing a oil and gas manufacturing IoT solution that is secured end-to-end following best practices. You will learn how to apply appropriate role-based access control permission to objects in this solution such as devices, sensors, cloud services and people. You will consider how to secure the network connecting all the devices, and how to monitor them using a SIEM. You will also work through zone assignments so that you have a clear picture of device security, gateway security, cloud services security. You will also provide Contoso guidance on defining lifecycles for particular components so that they have a plan that begins with initial deployment, to expected maintenance, to planned obsolesence and ultimately thru decommissioning of the device so that they can understand how Azure supports this. Additionally, you will perform some threat modeling to help WWI think about how they might handle: denial of service attacks, tampering, elevation of privelege, intrusion, information disclosure, man in the middle and protocol attacks against devices.   
At the end of this hands-on lab, you will be better able to implment a comprehensive and secure oil and gas manufacturing IoT solution.

#### Outline: Hands-on lab exercises
- Exercise 0: Before the hands-on lab
- Exercise 1: Creating the Digital Twins taxonomy
- Exercise 2: Querying the taxonomy and telemetry data
- Exercise 3: Applying Role Based Access Control
- Exercise 4: Monitoring solution security
- Exercise 5: Simulating an attack and threat mitigation
- Exercise 6: Managing the device lifecycle

## Azure services and related products
-	Azure Security Center
-	Azure Sentinel
-	Azure IoT Edge (including secure enclaves)
-	Azure IoT Hub
-	Azure Active Directory



## Related references
*This should be a list of and links to prereqs, architectural diagrams, supporting docs, or briefing decks related to the material.* 
- [MCW](https://github.com/Microsoft/MCW)
- https://docs.microsoft.com/en-us/azure/asc-for-iot/overview
