- **What is cloud computing?**
	- The on-demand delivery of compute power, database, storage, applications, and other IT resources through a cloud services platform through the internet with pay-as-you-go pricing
	- Traditionally, a developer looking to build an application had to procure, set up, and maintain physical infrastructure and the application. This is where cloud computing comes in.
	- A cloud services platform provides rapid access to flexible and low-cost IT resources that you can use to build and maintain software and databases, and create applications to delight customers. 
	- You can access as many resources as you need, almost instantly, and only pay for what you use. On-demand, pay-as-you-go access to services is fundamental to the cloud computing model.
- **Advantages of cloud computing**
	- **Pay as you go:** Pay only when you use computing resource, and only for how much you use.
	- **Benefit from massive economies of scale:** AWS aggregates usage from hundreds of thousands of customers in the cloud, which leads to higher economies of scale. This translates into lower pay-as-you-go prices.
	- **Stop guessing capacity:** When you make a capacity decision prior to deploying an application, you often end up either sitting on expensive idle resources or dealing with limited capacity. With cloud computing, you can access as much or as little capacity as you need, and scale up and down as required with only a few minutes notice.
	- **Increase speed and agility:** IT resources are only a click away, which means that you can reduce the time to make resources available to your developers from weeks to minutes. This dramatically increases agility for the organization, because the cost and time it takes to experiment and develop is significantly lower.
	- **Realize cost savings:** Companies can focus on projects that differentiate their business instead of maintaining data centers. With cloud computing, you can focus on your customers, rather than on the heavy lifting of racking, stacking, and powering physical infrastructure.
	- **Go global in minutes:** Applications can be deployed in multiple Regions around the world with a few clicks. You can provide lower latency and a better experience for your customers at a minimal cost.
- **What is AWS Cloud?**
	- AWS provides on-demand delivery of technology services through the Internet with pay-as-you-go pricing. This is known as cloud computing.
	- Encompasses a broad set of global cloud-based products that includes compute, storage, databases, analytics, networking, mobile, developer tools, management tools, IoT, security, and enterprise applications: on-demand, available in seconds, with pay-as-you-go pricing. Over 200 fully featured services available from data centers globally.
	- You can spin up a virtual machine, specifying the number of vCPU cores, memory, storage, and other characteristics i seconds, and pay for the infrastructure in per-second increments only while it is running. 
	- You can provision resources in the Region or Regions that best serve your specific use case. You can simply delete them too. 
- **On-premises and cloud computing**
	- Cloud computing emerged to help companies and organizations with the cost of maintaining a large physical presence of compute, storage, and networking equipment.
	- In an on-premises solution, an additional environment requires you to buy and install hardware, connect the necessary cabling, and more. This can be time consuming and expensive. If we run the application in the cloud, you can replicate an entire production environment, as often as needed, in a matter of minutes or even seconds.
	- Saves time during setup and removes undifferentiated heavy lifting.
- **IaaS, PaaS, and SaaS**
	- Each type of cloud service provides you with different levels of abstraction, control, flexibility, and management.
	- **Infrastructure as a Service (IaaS)**
		- Contains the basic building blocks for cloud IT, and typically provides access to networking features, computers (virtual or on dedicated hardware), and data storage space. Provides you with the highest level of flexibility and management control over your IT resources and is most like existing IT resources that many developers are familiar with today.
	- **Platform as a Service (PaaS)**
		- Removes the need for to manage underlying infrastructure (usually hardware and operating systems) and allows you to focus on the deployment and management of your applications. Be more efficient as  you don't need to worry about resource procurement, capacity planning, software maintenance, patching, or any of the other undifferentiated heavy lifting involved in running your application.
	- **Software as a Service (SaaS)**
		- Provides you with a completed product that is run and managed by the service provider. End-user applications. You only need to think about how you will use that piece of software.
- **Global infrastructure**
	- By putting your applications in closer proximity to your end users, you can reduce latency and improve the user experience.
	- AWS Cloud infrastructure is built around AWS Regions and Availability Zones. A Region is a physical location in the world where we have multiple Availability Zones.
- **Developer tools**
	-  Instead of physically managing infrastructure, you logically manage it, through the AWS Application Programming Interface (AWS API). When you create, delete, or change any AWS resource, you will use API calls to AWS to do that.
	- The AWS Management Console
		- Comprises a broad collection of service consoles for managing AWS resources
		- Don't need to worry about scripting or syntax
		- You may want to move away from manual deployment of AWS service since you became more familiar with AWS or are working in a production environment that requires a degree of risk management.
	- The AWS Command Line Interface (AWS CLI)
		- Open source tool that enables you to create and configure AWS services using commands in your command-line shell.
		- You can use AWS CloudShell, a browser-based shell that provides command-line access to AWS resources. CloudShell is pre-authenticated with your console credentials. Common development and operations tools are pre-installed, so no local installation or configuration is required.
		- One benefit of the CLI is that you can create single commands to create multiple AWS resources, which could help reduce the chance of human error when selecting and configuring resources.
		- With the CLI, you need to learn the proper syntax for forming commands, but as you script these commands, you make them repeatable.
	- IDE and IDE toolkits
		- AWS offers support for popular Integrated Development Environments (IDEs) and IDE toolkits so you can author, debug, and deploy your code on AWS from within your preferred environment. Supported IDEs and toolkits include [AWS Cloud9](https://aws.amazon.com/cloud9/?pg=cloudessentials), IntelliJ, PyCharm, Visual Studio, Visual Studio Code, Azure DevOps, Rider, and WebStorm.
	- AWS Software Development Kits (SDKs)
		- Allow you to interact with the AWS API programmatically. AWS creates and maintains SDKs for most popular programming languages, including those shown in the diagram.
- **Infrastructure as code (IaC)**
	-  AWS provides services that enable the creation, deployment, and maintenance of infrastructure in a programmatic, descriptive, and declarative way.
- **AWS CDK**
	- AWS Cloud Development Kit is a software development framework for defining cloud infrastructure in code and provisioning it through AWS CloudFormation.
	-  It provides high-level components called constructs that preconfigure cloud resources with proven defaults, so you can build cloud applications with ease.
	-  It also allows you to compose and share your own custom constructs incorporating your organization's requirements, helping you expedite new projects.
- **AWS CloudFormation**
	- CloudFormation helps you model and set up your AWS resources so that you can spend less time managing resources and more time focusing on your applications.
	- Once you create the template, CloudFormation takes care of provisioning and configuring those resources for you. You don't need to individually create and configure AWS resources and figure out what's dependent on what; CloudFormation handles that.
- **AWS responsibility**
	- Protecting and securing AWS Regions, Availability Zones, and data centers, down to the physical security of the buildings
	- Managing the hardware, software, and networking components that run AWS services, such as the physical servers, host operating systems, virtualization layers, and AWS networking components.
- **Customer responsibility**
	- Security in the cloud. You’re responsible for properly configuring the service and your applications, in addition to ensuring that your data is secure.
	- Some services require you to perform all the necessary security configuration and management tasks, while other more abstracted services require you to only manage the data and control access to your resources.
	- A key concept is that customers maintain complete control of their data and are responsible for managing the security related to their content.




































