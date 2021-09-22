# Node
## NodeJS & MySQL setup on Arm based processor on Oracle Cloud Infrastructure.

Here is a simplified digram of Linux Infrastructure set up required for the NodeJS and MySql set up 

![image](https://user-images.githubusercontent.com/89349920/130369775-5f0a6e41-a06b-498c-8557-afbe0f585d89.png)

### Free Tier: Install Node Express on an Oracle Linux Instance

In this tutorial, you use an Oracle Cloud Infrastructure Free Tier account to set up an Oracle Linux compute instance. Then, you install a Node Express application and access your new app from the internet. Finally, this tutorial covers all the steps necessary to set up a virtual network for your host and connect the host to the internet.

**Key tasks include how to:**

- Set up a compartment for your development work.

- Install your Oracle Linux instance and connect it to your Virtual Cloud Network (VCN).

- Set up an Oracle Cloud Infrastructure virtual cloud network and related network services required for your host to connect to the internet.

- Set up ssh encryption keys to access your Oracle Linux Server.

- Configure ingress rules for your VCN.

- Configure NodeJS with an Express framework on your instance.

**For additional information** 

Request and Manage Free Oracle Cloud Promotion
https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/signingup.htm


Launching your first Linux instance
https://docs.oracle.com/en-us/iaas/Content/GSG/Reference/overviewworkflow.htm

**To successfully complete this tutorial, you must have the following**

**Requirements**

An Oracle Cloud Infrastructure Free Tier account. Start for Free ( check the above link).
A MacOS, Linux, or Windows computer with ssh support installed.

**1. Set up a Compartment for Development**

Configure a compartment for your development.

- Create a Compartment
- Create a compartment for the resources that you create in this tutorial.

- [x] Log in to the Oracle Cloud Infrastructure Console. 

- [x] Open the navigation menu and click Identity & Security. Under Identity, click Compartments.

- [x] Click Create Compartment.

Fill in the following information:

Name: <your-compartment-name>
Description: Compartment for <your-description>.
Parent Compartment: <your-tenancy>(root)
Click Create Compartment.


**2. Install your Oracle Linux Instance**
Use the Create a VM Instance wizard to create a new compute instance.

The wizard does several things when installing the instance:

Creates and installs a compute instance running Oracle Linux.
  
Creates a VCN with the required subnet and components needed to connect your Oracle Linux instance to the internet.
  
Creates an ssh key pair you use to connect to your instance.
  
 - [x] Review Installation Steps

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

Availability domain: AD-3
Capacity type: On-demand capacity.
Fault domain: Oracle chooses the best placement.
  
  ![image](https://user-images.githubusercontent.com/89349920/130436891-542ad34e-c0b7-44be-ba1f-28a5416ec93a.png)

  
  ![image](https://user-images.githubusercontent.com/89349920/130370447-1d0ae23c-c095-4854-b37c-9ee7eb592518.png)

4. Review the Image and shape settings. Take the default values provided by the wizard.
  
  ![image](https://user-images.githubusercontent.com/89349920/130370473-b9587127-a0f1-4bd5-bd23-191fc4503cce.png)

  
Image & Shape
  
  - [X] Click on Edit On the image and shape 
  
  ![image](https://user-images.githubusercontent.com/89349920/130441923-f79ff002-cb93-4901-93d6-091fd7f828db.png)


  
- [x] Click on Change shape
  
  ![image](https://user-images.githubusercontent.com/89349920/130440367-8116627c-0265-48cb-a946-35f12a0752d2.png)

- [x] Select 
  
  Ampere - Arm based processor 
 
  ![image](https://user-images.githubusercontent.com/89349920/130440593-cd9acdbe-0dfb-449e-ae85-1e3e374fcbba.png)
  
  - [x] Click on the image : VM.Standard.A1.Flex
  - [x] Adjust the size of Number of OCPUs : 4 
  - [x] Amount of Memory(GB) : 24 ( This will get adjusted automatically based on the OCPUs selection)
  - [x] Click on Select Shape
  
  Note : In Always Free tier - 4 OCPUs/24GB is the maximum limit.
  
  ![image](https://user-images.githubusercontent.com/89349920/130440811-5ffb27c6-432c-4cb3-807d-ba3d2deee64d.png)
  
Here is the summary of the Image and Shape selection 

Image: Oracle Linux 7.9
Image build:  2021.07.27-0

Shape

Shape: VM.Standard.A1.Flex
OCPU count: 4
Memory (GB): 24
Network bandwidth (Gbps): 4
  


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

**You have successfully created an Oracle Linux instance.**
  
  **3. Enable Internet Access**
The Create a VM Instance wizard automatically creates a VCN for your instance. You add an ingress rule to your subnet to allow internet connections on port 3000.

Create an Ingress Rule for your VCN
Follow these steps to select your VCN's public subnet and add the ingress rule.

- [x] Open the navigation menu and click Networking, and then click Virtual Cloud Networks.
- [x] Select the VCN you created with your compute instance.
- [x] With your new VCN displayed, click <your-subnet-name> subnet link.
The public subnet information is displayed with the Security Lists at the bottom of the page. A link to the Default Security List for your VCN is displayed.

- [x] Click the Default Security List link.
The default Ingress Rules for your VCN are displayed.

- [x] Click Add Ingress Rules.
An Add Ingress Rules dialog is displayed.

- [x] Fill in the ingress rule with the following information.
- [x] Fill in the ingress rule as follows:

Stateless: Checked
Source Type: CIDR
Source CIDR: 0.0.0.0/0
IP Protocol: TCP
Source port range: (leave-blank)
Destination Port Range: 3000
Description: Allow HTTP connections
Click Add Ingress Rule.
Now HTTP connections are allowed. Your VCN is configured for Node Express.

**You have successfully created an ingress rule that makes your instance available from the internet.**
 
  **4. Create a Node Express Application**
  
Next, set up an Express framework on your Oracle Linux instance and then create and run a NodeJS application.

Install and Set up Node Express
Follow these steps to set up your instance and build your application:

- [x] Open the navigation menu and click Compute. Under Compute, click Instances.
- [x] Click the link to the instance you created in the previous step.
- [x] From the Instance Details page look in the Instance Access section. Copy the public IP address the system created for you. You use this IP address to connect to your instance.

- [x] Open a Terminal or Command Prompt window.
- [x] Change into the directory where you stored the ssh encryption keys you created for this tutorial.
- [x] Connect to your instance with this SSH command:
  
 ```ssh -i <your-private-key-file> opc@<x.x.x.x>```
  
  Since you identified your public key when you created the instance, this command logs you into your instance. You can now issue sudo commands to install and start your server.
 
  ## How to connect to your Unix Instance ( from Windows 10) - Refer to the link below
  
  https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/testingconnection.htm

  - [x] Enable HTTP connection on port 3000.
  
 ```sudo firewall-cmd --permanent --add-port=3000/tcp```
 ```sudo firewall-cmd --reload```
  
  - [x] Install the latest version of NodeJS.

 ```sudo yum update```
 ```sudo yum install -y docker-ce```
  
Try a react 'Hello World App'  - this will start a react "hello world" on port 3000 which you should be able to connect to with the public IP address of the compute instance. 
  
  
```mkdir ~/repos```
```cd ~/repos```
```npx create-react-app my-react-docker-app```
```cd my-react-docker-app/```
```npm start```

  Test the application using a browser:
  From a browser, connect to the public IP address assigned to your instance: http://<x.x.x.x>:3000
  
  Install NodeJS Docker image on Oracle Linux 7
  
```sudo yum-config-manager --enable ol7_developer_EPEL```
```sudo yum-config-manager --enable ol7_developer```
```sudo yum install -y docker-ce```

Now start the docker service
  
```sudo service docker start```

Update privilage for the default oracle account 'opc' to run the docker service
  
```sudo usermod -a -G docker opc```
  
To check the docker process is running you must logoff the session and login again ( using ssh)

Check thet the dcoker process is running
   
 ```docker ps -a```
  
  Check the version of the Node
  
 ```node -v```
  
  Now let's create a react application
  
```mkdir ~/repos```
```cd ~/repos```
```npx create-react-app my-react-docker-app```
```cd my-react-docker-app/```
```npm start```
  
Test the application using a browser:
From a browser, connect to the public IP address assigned to your instance: http://<x.x.x.x>:3000
  
This should create a simple landing page like this ...
  
![image](https://user-images.githubusercontent.com/89349920/130466846-63cae951-bda8-419b-ae6b-8bbea3b307a8.png)
  
Next , Ctrl-C to exit the running server ...
then create a Dockerfile in the my-react-docker-app directory by using nano editor

```nano Dockerfile```

Update with following values 
  
FROM node:alpine

WORKDIR /app

COPY package.json /app

RUN yarn install

COPY . /app

CMD ["yarn", "run", "start"]
  
and then save with Ctrl-X
  
Next , execute this to build a docker image that can be executed ...
  
```docker build -t react-app:latest .```

After the successful completion , run this
  
```docker run --rm -d -p 3000:3000 --hostname react --name react react-app:latest```

The above command runs the image "react-app:latest" with the hostname react with the port 3000 (exposed to the compute) to the port 3000 (locally used by react)
with the process running as a daemon process

Check the react app process is running 
  
```docker ps -a```
  
  ![image (1)](https://user-images.githubusercontent.com/89349920/130469425-c192bb58-7687-4f65-833d-47a124dee08d.png)
  
Test the application using a browser:
From a browser, connect to the public IP address assigned to your instance: http://<x.x.x.x>:3000
  
Test the application from a broser on a mobile phone
  
![Screenshot_20210820-224943_Samsung Internet](https://user-images.githubusercontent.com/89349920/130469819-6b03f85f-e9d6-4e66-ae08-7bb2c166e185.jpg)
  
You have a React Mobile app !
  
# How to Use the MySQL Images 
## Downloading a MySQL Server Docker Image

**To download the MySQL Community Edition image, run this command:**

```docker pull mysql/mysql-server:8.0.13```
  
**Starting a MySQL Server Instance**

```docker run --name=mysql -d mysql/mysql-server:8.0.13```
  
The ```--name``` option, for supplying a custom name for your server container (```mysql1``` in the example), is optional; if no container name is supplied, a random one is generated. If the Docker image of the specified name and tag has not been downloaded by an earlier ```docker pull``` or ```docker run command```, the image is now downloaded. After download completes, initialization for the container begins, and the container appears in the list of running containers when you run the ```docker ps``` command; for example:
  
Once agaian check the React and MySql docker processing are running
  
```docker pa -a```
  
  ![image (2)](https://user-images.githubusercontent.com/89349920/130474005-53177e1c-1ff7-4d02-9afd-cae0785909cc.png)
  
**Connecting to MySQL Server from within the Container**
  
Once the server is ready, you can run the mysql client within the MySQL Server container you just started and connect it to the MySQL Server. Use the ```docker exec -it``` command to start a ```mysql``` client inside the Docker container you have started, like this:

```docker exec -it mysql1 mysql -uroot -p```
  
When asked, enter the generated root password (see the instructions above on how to find it). Because the ```MYSQL_ONETIME_PASSWORD``` option is true by default, after you have connected a ```mysql``` client to the server, you must reset the server root password by issuing this statement:
  
```docker log mysql```
```docker logs 2>&1 | grep GENERATED```
```docker exec -it mysql1 mysql -uroot -p``` - enter GENERATED ROOT PASSWORD
  
  
  mysql> ```ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';```
  
  For mnore on MySql and MySql Programs check this link 
  
  https://dev.mysql.com/doc/refman/8.0/en/mysql.html 
  
  
  To complete the Infrastructure environment for development , suggest Installing Git on the same server 
  
  ```yum install -y git```

The NodeJS Raect and MySql development environment is now ready 



  
