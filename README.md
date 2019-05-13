# Securing the IoT end-to-end
World Wide Importers (WWI) provides an e-commerce platform that provides artisans, makers and crafters a marketplace to sell their goods to consumers. In their 20 years in business, they have grown from a small mail-order business, to a 5,000 person company that is part art gallery and part auction house. They have recently acquired moved into a new campus that will serve as their headquarters. In an effort to improve productivity and employee satisfication onsite, they would like to invest in making their building "smart". Company leadership is very excited by the opportunity, but only as long as the Chief Security Officer is satisfied that all of the "things" involved in the smart building can be properly secured. 

They would like to start by building a proof of concept around a single building that has 5 floors, and focus on how they would deploy, manage and secure two different types of sensors in the common areas and conference rooms: motion detectors and carbon monoxide detectors. The simple use cases they have in mind are:
- Enabling employees to locate comfortable meeting venues (e.g., because there is little motion and the air quality is high).
- Enabling security to identify suspicious activity (e.g., lots of motion or unusually heavy room use as deemed by air quality)

As their e-commerce platform already runs in Azure, they are interested in understanding how Azure could help them with a secure IoT environment.  

## Target audience
-	IoT Engineers
-	Network Security Administrators
-	Network Engineers

## Abstract

### Workshop
In this workshop, you will look at the process for designing and implementating a smart building IoT solution that is secured end-to-end following best practices. 

At the end of this workshop, you will be better able to architect a comprehensive and secure smart building solution.

![Solution taxonomy using Digital Twins](Media/digital-twins-spatial-graph-building.png)

### Whiteboard design session
In this whiteboard design session, you will look at the process for designing a smart building IoT solution that is secured end-to-end following best practices. You will learn to define the ontology representing all virtual and real-world assets involved in the solution, and how to apply appropriate role-based access control permission to objects in this taxonomy such as buildings, devices, sensors and people. You will consider how to secure the network connecting all the devices, and how to monitor them using a SIEM. You will also work through zone assignments so that you have a clear picture of device security, gateway security, cloud services security. You will also provide WWI guidance on defining lifecycles for particular components so that they have a plan that begins with initial deployment, to expected maintenance, to planned obsolesence and ultimately thru decommissioning of the device so that they can understand how Azure supports this. Additionally, you will perform some threat modeling to help WWI think about how they might handle: denial of service attacks, tampering, elevation of privelege, intrusion, information disclosure, man in the middle and protocol attacks against devices.  

At the end of this whiteboard design session, you will be better able to architect a comprehensive and secure smart building solution.

#### Outline: Key Concerns for Cutomer situation ####
- Can we use Azure Sentinel with an IoT solution?
- Is Digital Twins the right service for our PoC?
- What tools can we use to monitor network traffic?
- How can we provide a secure identity to each of our devices?
- How can we proactively guard against attacks to our smart building?
- What devices should we prefer? Does Azure provide any support for devices that are secure and maintainable?

### Hands-on lab 
In this hands-on lab, you will look at the process for implementing a smart building IoT solution that is secured end-to-end following best practices. You will learn to define the ontology representing all virtual and real-world assets involved in the solution, and how to apply appropriate role-based access control permission to objects in this taxonomy such as buildings, devices, sensors and people. You will consider how to secure the network connecting all the devices, and how to monitor them using a SIEM. You will also work through zone assignments so that you have a clear picture of device security, gateway security, cloud services security. You will also provide WWI guidance on defining lifecycles for particular components so that they have a plan that begins with initial deployment, to expected maintenance, to planned obsolesence and ultimately thru decommissioning of the device so that they can understand how Azure supports this. Additionally, you will perform some threat modeling to help WWI think about how they might handle: denial of service attacks, tampering, elevation of privelege, intrusion, information disclosure, man in the middle and protocol attacks against devices.  

At the end of this hands-on lab, you will be better able to implment a comprehensive and secure smart building solution.

#### Outline: Hands-on lab exercises
- Exercise 0: Before the hands-on lab
- Exercise 1: Creating the Digital Twins taxonomy
- Exercise 2: Querying the taxonomy and telemetry data
- Exercise 3: Applying Role Based Access Control
- Exercise 4: Monitoring solution security
- Exercise 5: Simulating an attack and threat mitigation
- Exercise 6: Managing the device lifecycle

## Azure services and related products
-	Azure Sentinel
-	Azure Digital Twins
-	Azure IoT Hub
-	Azure Active Directory
-	Azure Sphere


## Related references
*This should be a list of and links to prereqs, architectural diagrams, supporting docs, or briefing decks related to the material.* 
- [MCW](https://github.com/Microsoft/MCW)
- [Quickstart: Find available roomws by using Azure Digital Twins](https://docs.microsoft.com/en-us/azure/digital-twins/quickstart-view-occupancy-dotnet)