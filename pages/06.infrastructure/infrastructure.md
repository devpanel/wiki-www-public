---
herotitle: 'YOUR Infrastructure'
herosubtitle: 'This is all the stuff DevPanel sets up for you in YOUR AWS account'
map:
    image: devpanel-infrastructure-2019.png
    markers:
        -
            x: '4'
            'y': '77'
            text: 'using Cloud Formation, DevPanel automates the setup and configuration of all this infrastructure in your AWS account.'
        -
            x: '6'
            'y': '26'
            text: 'when you deploy your site/app to production, we use Route53 (R53) to manage your DNS. We generate an SSL certificate for your site/app using the Amazon Certificate Manager and we setup and configure the WAF, the Web Application Firewall, to protect your site from malicious attacks.'
        -
            x: '0'
            'y': '38'
            text: 'as users hit your site/app, they first have to pass the WAF’s safety checks. This stops any malicious attacks on your site/app.'
        -
            x: '0'
            'y': '38'
            text: 'If the incoming request is determined to be safe, then it’s sent to the Elastic Load Balancer (ELB) which determines which machine (EC2) and Availability Zone (AZ) the request should be routed to based on the load of each machine…'
        -
            x: '71'
            'y': '39'
            text: "If the load is reaching maximum capacity on all the machines, then a Cloud Watch Alarm will trigger a creation of a new machine. \r\n\r\nIf the load stays below a specified threshold for an extended period of time, then another Cloud Watch Alarm will trigger the removal of extra machines.\r\n\r\nThis is how auto-scaling saves you money. By shrinking your infrastructure when you don’t have traffic and by growing your infrastructure as needed."
        -
            x: '70'
            'y': '21'
            text: "inside this EC2, we use Elastic Container Service (ECS) to create and manage Docker containers. \r\n\r\nYour applications run inside Docker containers. \r\n\r\nECS, itself, is a managed service that will create and destroy containers as needed so we don’t need to micromanage the containers. We just let ECS auto-scale the containers as needed."
        -
            x: '62'
            'y': '55'
            text: "each container relies on shared services like IAM, Amazon S3, EFS, RDS Aurora, and Parameter Store. \r\n\r\nWhatever a container needs, it gets from these services."
        -
            x: '76'
            'y': '6'
            text: "CloudWatch and Lambda are used to monitor and fix all the AWS resources in your account. \r\n\r\nCloudWatch notifies DevPanel if anything is going wrong and then we call Lambda functions to fix things before you encounter downtime."
        -
            x: '26'
            'y': '5'
            text: "Notice that we’re running duplicate setup in two Availability Zones (AZ1 & AZ2.) \r\n\r\nThis way, if there’s a problem with one data center (AZ,) then the traffic is automatically directed to the other Availability Zone. \r\n\r\nThis gives you a highly available system to start with. \r\n\r\nYou don’t have to do anything."
        -
            x: '13'
            'y': '77'
            text: "And finally, when we find problems with our setup and/or our scripts, we’ll push out the fixes ASAP. \r\n\r\nBTW, all our scripts are open source and you’re welcome to examine and audit them. In fact we encourage it. \r\n\r\nBut, if you do find something, please contact us directly and we’ll work with you to not only fix the problem for you but for all our customers."
        -
            x: '20'
            'y': '54'
            text: 'Oh, we’re still working on adding these…'
aws:
    ins:
        -
            title: 'AWS Certificate Manager'
            summary: 'Easily provision, manage, and deploy public and private SSL/TLS certificates for use with AWS services and your internal connected resources.'
            icon: aws-cert.svg
            link: 'https://aws.amazon.com/certificate-manager/'
            text: "AWS Certificate Manager is a service that lets you easily provision, manage, and deploy public and private Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificates for use with AWS services and your internal connected resources. SSL/TLS certificates are used to secure network communications and establish the identity of websites over the Internet as well as resources on private networks. AWS Certificate Manager removes the time-consuming manual process of purchasing, uploading, and renewing SSL/TLS certificates.\r\n\r\nDevPanel uses the AWS Certificate Manager to generate SSL certificates for your production/live sites. Using AWS Certificate Manager for this costs nothing and removes the hassle of purchasing, renewing and installing SSL certificates every few years. AWS Certificate Manager keeps your certificate up-to-date… always. This is another way DevPanel saves you time, effort and money."
        -
            title: 'Amazon Virtual Private Cloud'
            summary: 'Provision a logically isolated section of the Amazon Web Services (AWS) Cloud where you can launch AWS resources in a virtual network that you define.'
            icon: aws-vpc-1.svg
            text: "Amazon Virtual Private Cloud (Amazon VPC) lets you provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways. You can use both IPv4 and IPv6 in your VPC for secure and easy access to resources and applications.\r\n\r\nDevPanel sets up a VPC under your account to isolate and secure most of the infrastructure that we setup for you. We further separate the VPC into several subnets (like public subnets, frontend subnet, backend subnet, and database subnet) to further isolate services. "
        -
            title: 'Elastic Load Balancing'
            summary: 'Achieve fault tolerance for any application by ensuring scalability, performance, and security.'
            icon: aws-elb.svg
            text: "Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and Lambda functions. It can handle the varying load of your application traffic in a single Availability Zone or across multiple Availability Zones. Elastic Load Balancing offers three types of load balancers that all feature the high availability, automatic scaling, and robust security necessary to make your applications fault tolerant.\r\n\r\n##### **Application Load Balancer**  \r\n\r\nApplication Load Balancer is best suited for load balancing of HTTP and HTTPS traffic and provides advanced request routing targeted at the delivery of modern application architectures, including microservices and containers. Operating at the individual request level (Layer 7), Application Load Balancer routes traffic to targets within Amazon Virtual Private Cloud (Amazon VPC) based on the content of the request.\r\n\r\n##### **Network Load Balancer**  \r\n\r\nNetwork Load Balancer is best suited for load balancing of Transmission Control Protocol (TCP) and Transport Layer Security (TLS) traffic where extreme performance is required. Operating at the connection level (Layer 4), Network Load Balancer routes traffic to targets within Amazon Virtual Private Cloud (Amazon VPC) and is capable of handling millions of requests per second while maintaining ultra-low latencies. Network Load Balancer is also optimized to handle sudden and volatile traffic patterns.\r\n\r\n##### **Classic Load Balancer**  \r\n\r\nClassic Load Balancer provides basic load balancing across multiple Amazon EC2 instances and operates at both the request level and connection level. Classic Load Balancer is intended for applications that were built within the EC2-Classic network.\r\n\r\nDevPanel sets up and configures two of the three types of load balancers: the Application Load Balancer (ALB) and the Network Load Balancer (NLB.) This is to provide balanced traffic management at the application layer (layer 7) and the network layer (layer 4.) Each is optimized for particular use case so that’s why we use both. Most companies still use the Classic (Legacy) Load Balancer… When Amazon comes out with new technology, DevPanel will integrate that ASAP so you and your company can benefit from it ASAP. This is another benefit of using DevPanel rather than rolling your own solution.\r\n"
        -
            title: 'Amazon Elastic Container Registry'
            summary: 'Easily store, manage, and deploy container images.'
            icon: aws-ecr.svg
            text: "Amazon Elastic Container Registry (ECR) is a fully-managed Docker container registry that makes it easy for developers to store, manage, and deploy Docker container images. Amazon ECR is integrated with Amazon Elastic Container Service (ECS), simplifying your development to production workflow. Amazon ECR eliminates the need to operate your own container repositories or worry about scaling the underlying infrastructure. Amazon ECR hosts your images in a highly available and scalable architecture, allowing you to reliably deploy containers for your applications. \r\n\r\nDevPanel uses ECR to store your application images so additional containers can be deployed instantly when your application needs to scale up. With Amazon ECR, there are no upfront fees or commitments. You pay only for the images you store in ECR."
        -
            title: 'Amazon Elastic File System'
            summary: 'Scalable, elastic, cloud-native file system for Linux.'
            icon: aws-ec2.svg
            text: "Amazon Elastic File System (Amazon EFS) provides a simple, scalable, elastic file system for Linux-based workloads for use with AWS Cloud services and on-premises resources. It is built to scale on demand to petabytes without disrupting applications, growing and shrinking automatically as you add and remove files, so your applications have the storage they need – when they need it. It is designed to provide massively parallel shared access to thousands of Amazon EC2 instances, enabling your applications to achieve high levels of aggregate throughput and IOPS with consistent low latencies. Amazon EFS is a fully managed service that requires no changes to your existing applications and tools, providing access through a standard file system interface for seamless integration. Amazon EFS is a regional service storing data within and across multiple Availability Zones (AZs) for high availability and durability. You can access your file systems across AZs, regions, and VPCs and share files between thousands of Amazon EC2 instances and on-premises servers via AWS Direct Connect or AWS VPN.\r\n\r\nDevPanel uses EFS for storing your application code. All your applications sit on EFS. This way, when changes are deployed to any application, those changes are reflected on all containers instantly without any risk of lag time between updates."
        -
            title: 'Amazon Relational Database Service (RDS)'
            summary: 'Set up, operate, and scale a relational database in the cloud with just a few clicks.'
            icon: aws-rds.svg
            text: "Amazon Relational Database Service (Amazon RDS) makes it easy to set up, operate, and scale a relational database in the cloud. It provides cost-efficient and resizable capacity while automating time-consuming administration tasks such as hardware provisioning, database setup, patching and backups. It frees you to focus on your applications so you can give them the fast performance, high availability, security and compatibility they need.\r\n\r\nDevPanel sets up, configures and secures RDS database for you in your own AWS account."
        -
            title: 'Amazon Aurora'
            summary: 'MySQL and PostgreSQL-compatible relational database built for the cloud. Performance and availability of commercial-grade databases at 1/10th the cost.'
            icon: aws-rds.svg
            text: "Amazon Aurora is a MySQL and PostgreSQL-compatible relational database built for the cloud, that combines the performance and availability of traditional enterprise databases with the simplicity and cost-effectiveness of open source databases.\r\n\r\nAmazon Aurora is up to five times faster than standard MySQL databases and three times faster than standard PostgreSQL databases. It provides the security, availability, and reliability of commercial databases at 1/10th the cost. Amazon Aurora is fully managed by Amazon Relational Database Service (RDS), which automates time-consuming administration tasks like hardware provisioning, database setup, patching, and backups.\r\n\r\nAmazon Aurora features a distributed, fault-tolerant, self-healing storage system that auto-scales up to 64TB per database instance. It delivers high performance and availability with up to 15 low-latency read replicas, point-in-time recovery, continuous backup to Amazon S3, and replication across three Availability Zones (AZs).\r\n\r\nDevPanel uses Aurora exclusively - because it’s so freaking awesome! Your application can be customized to use Aurora Serverless and/or encrypted Amazon Aurora instance with AWS Key Management Service (KMS) for having your data be encrypted at rest and in transit."
        -
            title: 'Amazon CloudWatch'
            summary: 'Complete visibility of your cloud resources and applications.'
            icon: aws-cloudwatch.svg
            text: "Amazon CloudWatch is a monitoring and management service built for developers, system operators, site reliability engineers (SRE), and IT managers. CloudWatch provides you with data and actionable insights to monitor your applications, understand and respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health. CloudWatch collects monitoring and operational data in the form of logs, metrics, and events, providing you with a unified view of AWS resources, applications and services that run on AWS, and on-premises servers. You can use CloudWatch to set high resolution alarms, visualize logs and metrics side by side, take automated actions, troubleshoot issues, and discover insights to optimize your applications, and ensure they are running smoothly.\r\n\r\nDevPanel configures CloudWatch with alarms and triggers for auto-scaling (up and down) and to trigger various maintenance and auto-healing automation tasks."
        -
            title: 'Amazon Simple Email Service'
            summary: 'Coming Soon!'
            icon: aws-ses.svg
            text: 'Flexible, affordable, and highly-scalable email sending and receiving platform for businesses and developers.'
        -
            title: 'AWS Cloud​Formation'
            icon: aws-cloudformation.svg
            text: "AWS CloudFormation provides a common language for you to describe and provision all the infrastructure resources in your cloud environment. CloudFormation allows you to use a simple text file to model and provision, in an automated and secure manner, all the resources needed for your applications across all regions and accounts. This file serves as the single source of truth for your cloud environment.\r\n\r\nEverything deployed by DevPanel in a user’s account is done through CloudFormation. We create CloudFormation scripts and then execute them to setup all the infrastructure. All our CloudFormation scripts are open source and you’re welcome to examine and improve them."
        -
            title: 'Amazon S3'
            summary: 'Object storage built to store and retrieve any amount of data from anywhere.'
            icon: aws-s3.svg
            text: "Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance. This means customers of all sizes and industries can use it to store and protect any amount of data for a range of use cases, such as websites, mobile applications, backup and restore, archive, enterprise applications, IoT devices, and big data analytics. Amazon S3 provides easy-to-use management features so you can organize your data and configure finely-tuned access controls to meet your specific business, organizational, and compliance requirements. Amazon S3 is designed for 99.999999999% (11 9's) of durability, and stores data for millions of applications for companies all around the world.\r\n\r\n\r\nJust look at those 9s! DevPanel currently only uses S3 for backups and snapshots. Custom apps can be configured to use S3 extensively for many other purposes."
        -
            title: 'AWS WAF - Web Application Firewall'
            summary: 'Protect your web applications from common web exploits.'
            icon: aws-waf.svg
            text: "AWS WAF is a web application firewall that helps protect your web applications from common web exploits that could affect application availability, compromise security, or consume excessive resources. AWS WAF gives you control over which traffic to allow or block to your web applications by defining customizable web security rules. You can use AWS WAF to create custom rules that block common attack patterns, such as SQL injection or cross-site scripting, and rules that are designed for your specific application. New rules can be deployed within minutes, letting you respond quickly to changing traffic patterns. Also, AWS WAF includes a full-featured API that you can use to automate the creation, deployment, and maintenance of web security rules.\r\n\r\nDevPanel configures AWS WAF to protect your production sites from OWASP Top 10. This protects your sites from things like Cross Site Scripting (XSS) and SQL Injections. With AWS WAF you pay only for what you use. AWS WAF pricing is based on how many rules you deploy and how many web requests your web application receives. There are no upfront commitments."
        -
            title: 'AWS Lambda'
            summary: 'AWS Lambda lets you run code without provisioning or managing servers. You pay only for the compute time you consume - there is no charge when your code is not running.'
            icon: aws-lambda.svg
            text: "With Lambda, you can run code for virtually any type of application or backend service - all with zero administration. Just upload your code and Lambda takes care of everything required to run and scale your code with high availability. You can set up your code to automatically trigger from other AWS services or call it directly from any web or mobile app.\r\n\r\nDevPanel uses Lambda for notification and automation. Other uses for Lambda are in currently in development. We plan to leverage Lambda heavily going forward."
media_order: 'aws-autoscaling.png,aws-cloudwatch.png,aws-ec2.png,aws-elasticloadbalancing.png,aws-rds.png,aws-s3.png,ECS.png,vpc_ntier.png,vpc_ntier_npbg.png,aws-cloudformation.svg,aws-elb.svg,aws-cert.svg,aws-cloudwatch.svg,aws-s3.svg,aws-rds.svg,aws-ses.svg,aws-lambda.svg,aws-ecr.svg,aws-waf.svg,aws-vpc-1.svg,aws-cloudfront.svg,aws-ec2.svg,SKL_201902021314.png'
title: Infrastructure
visible: false
body_classes: infrastructure
access:
    site.login: true
    admin.login: true
---

