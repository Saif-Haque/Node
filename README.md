# Node
NodeJS & MySQL Infrastructure setup on Oracle Cloud Infrastructure.

Here is a simplified digram of Linux Infrastructure set up required for the NodeJS and MySql set up 

![image](https://user-images.githubusercontent.com/89349920/130369775-5f0a6e41-a06b-498c-8557-afbe0f585d89.png)

Free Tier: Install Node Express on an Oracle Linux Instance

In this tutorial, you use an Oracle Cloud Infrastructure Free Tier account to set up an Oracle Linux compute instance. Then, you install a Node Express application and access your new app from the internet. Finally, this tutorial covers all the steps necessary to set up a virtual network for your host and connect the host to the internet.

Key tasks include how to:

Set up a compartment for your development work.

Install your Oracle Linux instance and connect it to your Virtual Cloud Network (VCN).

Set up an Oracle Cloud Infrastructure virtual cloud network and related network services required for your host to connect to the internet.

Set up ssh encryption keys to access your Oracle Linux Server.

Configure ingress rules for your VCN.

Configure NodeJS with an Express framework on your instance.

For additional information 

Request and Manage Free Oracle Cloud Promotions
https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/signingup.htm


Launching your first Linux instance
https://docs.oracle.com/en-us/iaas/Content/GSG/Reference/overviewworkflow.htm

o successfully complete this tutorial, you must have the following:

Requirements

An Oracle Cloud Infrastructure Free Tier account. Start for Free ( check the above link).
A MacOS, Linux, or Windows computer with ssh support installed.

1. Set up a Compartment for Development
Configure a compartment for your development.

Create a Compartment
Create a compartment for the resources that you create in this tutorial.

Log in to the Oracle Cloud Infrastructure Console.

Open the navigation menu and click Identity & Security. Under Identity, click Compartments.

Click Create Compartment.

Fill in the following information:

Name: <your-compartment-name>
Description: Compartment for <your-description>.
Parent Compartment: <your-tenancy>(root)
Click Create Compartment.


2. Install your Oracle Linux Instance
Use the Create a VM Instance wizard to create a new compute instance.

The wizard does several things when installing the instance:

Creates and installs a compute instance running Oracle Linux.
  
Creates a VCN with the required subnet and components needed to connect your Oracle Linux instance to the internet.
  
Creates an ssh key pair you use to connect to your instance.
  
  Review Installation Steps

  To get started installing your instance with the Create a VM Instance wizard, follow these steps:

1. From the main landing page, select Create a VM Instance wizard
  
  ![image](https://user-images.githubusercontent.com/89349920/130370355-ccc9abd8-4d8b-4979-a21f-17b2eb3bb8cd.png)

  The Create Compute Instance page is displayed. It has a section for Placement, Image and shape, Networking, Add SSH keys, and Boot volume.
  
2. Choose the Name and Compartment.
Initial Options

Name: <name-for-the-instance>
Create in compartment: <your-compartment>
Enter a value for the name or leave the system supplied default.
  
3. Review the Placement settings. Take the default values provided by the wizard.
  ![image](https://user-images.githubusercontent.com/89349920/130370430-9714d508-6833-40e9-a4d2-41e799fe5354.png)

Placement

Availability domain: AD-1
Capacity type: On-demand capacity.
Fault domain: Oracle chooses the best placement.
  
  ![image](https://user-images.githubusercontent.com/89349920/130370447-1d0ae23c-c095-4854-b37c-9ee7eb592518.png)

4. Review the Image and shape settings. Take the default values provided by the wizard.
  
  ![image](https://user-images.githubusercontent.com/89349920/130370473-b9587127-a0f1-4bd5-bd23-191fc4503cce.png)

  
Image

Image: Oracle Linux 7.9
Image build: 2020.11.10-1

Shape

Shape: VM.Standard.A1.Flex
OCPU count: 4
Memory (GB): 24
Network bandwidth (Gbps): 0.48
  
  ![image](https://user-images.githubusercontent.com/89349920/130370507-7f202c9f-d174-4525-ad27-13fc730772f5.png)

5. Review the Networking settings. Take the default values provided by the wizard.
  ![image](https://user-images.githubusercontent.com/89349920/130370536-77bc2ccc-7d3a-48c3-abaa-0b84620a5137.png)
  
Virtual cloud network: vcn-<date>-<time>
Subnet: vcn-<date>-<time>
Assign a public IPv4 address: Yes
  
6. Review the Add SSH keys settings. Take the default values provided by the wizard.
  
Select the Generate a key pair for me option.
Click Save Private Key and Save Public Key to save the private and public SSH keys for this compute instance.
If you want to use your own SSH keys, select one of the options to provide your public key.

  ![image](https://user-images.githubusercontent.com/89349920/130370605-298082f3-dc77-4bd0-a89a-dbafa2047fd7.png)

7. Review the Boot volume settings. Take the default values provided by the wizard.
   Leave all check boxes unchecked.

8. Click Create to create the instance. Provisioning the system might take several minutes.
   You have successfully created an Oracle Linux instance.



