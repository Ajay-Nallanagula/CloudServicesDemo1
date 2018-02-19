Azure App Service, Virtual Machines, Service Fabric, and Cloud Services comparison
https://docs.microsoft.com/en-us/azure/app-service/choose-web-site-cloud-service-vm

1.Azure Cloud Services is an example of a platform as a service (PaaS). Like Azure App Service, this technology is designed to support applications that are scalable, reliable, and inexpensive to operate.

2. Basic difference between AppService and Cloud Services is in cloud services you will have more control over the VM's .

3. Azure offers fault management, automatic patching, SPs, security fixes with cloud services

https://cloudacademy.com/blog/microsoft-azure-app-service-virtual-machines/

Basics of Azure Cloud Services:https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-choose-me
a) Web Role: Automatically deploys and hosts your app through IIS.
   Worker Role : Does not use IIS, and runs your app standalone.
   
b) all the VMs in a single application run in the same cloud service. Users access the application through a single public IP address, with requests automatically load balanced across the application's VMs
   
c) With IaaS, such as Azure Virtual Machines, you first create and configure the environment your application runs in. Then you deploy your application into this environment. You're responsible for managing much of this world, by doing things such as deploying new patched versions of the operating system in each VM. In PaaS, by contrast, it's as if the environment already exists. All you have to do is deploy your application. Management of the platform it runs on, including deploying new versions of the operating system, is handled for you
   
d) The PaaS nature of Azure Cloud Services has other implications, too. One of the most important is that applications built on this technology should be written to run correctly when any web or worker role instance fails. To achieve this, an Azure Cloud Services application shouldn't maintain state in the file system of its own VMs. Unlike VMs created with Virtual Machines, writes made to Azure Cloud Services VMs aren't persistent. There's nothing like a Virtual Machines data disk. Instead, an Azure Cloud Services application should explicitly write all state to Azure SQL Database, blobs, tables, or some other external storage. Building applications this way makes them easier to scale and more resistant to failure, which are both important goals of Azure Cloud Services.
   
e) With Azure Cloud Services, you don't create virtual machines. Instead, you provide a configuration file that tells Azure how many of each you'd like, such as "three web role instances" and "two worker role instances

What is a Package ? How do you deploy it in Azure

Way 1:
You can create a package i.e is build package which can be deployed in staging or production 
This can be create using Visual studio --> Goto azure cloud services project , this have a cloud icon where roles are been created
right click and you should see the package option

Select the service configuration and build configuration (Release, Debug) you want to package. Then hit on Package. This will build all the necessary projects for your cloud solution. Once finished, it will popup a window with 2 files: a cspkg and a cscfg. The cspkg can be opened with any zip software by the way

Go to Azure portal. Select "Cloud Services". Select your cloud service name. Clic on "UPLOAD A NEW PRODUCTION DEPLOYMENT". Select your cspkg and cscfg files form step 2. Give a name to your deployment.

Way 2:
Publish from Visual Studio. To save the hustle right click on your Cloud project and select "Publish". Apply the necessary settings (Cloud service -this will populate automatically-, Environment, Release...as in the previous way. Make sure you go to Advanced settings to select the correct storage account if you got multiple. Hit Next, and the Publish. Visual Studio will do all the hard work for you.
https://stackoverflow.com/questions/15618251/how-to-create-a-cloud-service-package-cspkg-and-cloud-service-configuration-f

Note : When the cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center. Bandwidth within a data center is free.

What are affinity groups in Azure : http://pipe2text.com/?page_id=1715
Azure affinity groups provide a mechanism to minimize the distance between resources in a data center, which can reduce latency. This tutorial does not use affinity groups. For more information

Disadvantages of Cloud Services : https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-deployment-model
Cloud Services does not support Resource Manager deployment model.
NOTE : However, just existing within a resource group does not mean that the resource has been converted to the Resource Manager model.