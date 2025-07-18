# Set-Up-and-Monitor-a-WordPress-Instance
##Introduction
This project demonstrates the design and deployment of a WordPress application on AWS.
##Project Objectives
Set up a live WordPress instance to publish blogs.


Make it so that the WordPress instance can be be developed and tested without affecting the live blog


Configure the WordPress instance so it is only available for development and testing from 9AM-6PM


##Architecture Overview
Frontend: Amazon EC2 instances hosting WordPress, distributed by an Application Load Balancer.


Storage: Amazon EFS (Elastic File System) for shared WordPress content.


Database: Amazon RDS (managed MySQL) with read replicas for performance and reliability.


Networking: Deployed across multiple Availability Zones for high availability, with security groups restricting access.


Automation: Infrastructure provisioned via AWS CloudFormation templates.


Scalability: Managed using Auto Scaling Groups.


Monitoring: Route 53 health checks and CloudWatch alarms.


Cost Efficiency: Auto-shutdown of development/test environments outside business hours.



##Implementation Steps
1. Create a CloudFormation Stack
Created a reusable CloudFormation template to deploy all core resources (EC2, RDS, EFS, security groups).


Defined AWS IAM roles and policies for least-privilege access.


2. Create an AMI of the WordPress instance
Used Free Tier-eligible Amazon Linux 2 AMI.


Added a User Data script in the Launch Template to install WordPress.


Script included steps to download and configure WordPress, set permissions, and start services.


3. Configure Auto Scaling to launch a new WordPress instance
Configured an Auto Scaling Group with the Launch Template, distributing instances across different Availability Zones.


Set scaling policies based on CPU utilization and network metrics.


Integrated with an Application Load Balancer for traffic distribution.



4. Configure the new WordPress instance to shut down  
automatically
Used AWS Systems Manager Quick Setup with a custom tag (AutoShutdown = True) to automatically stop the development/test EC2 instance during non-business hours.



5. Monitor the instance using Availability Monitoring feature of the R53
Enabled Route 53 health checks for public endpoints.


Configured CloudWatch alarms to alert on resource failures or unusual activity.


##Key Takeaways and Skills Developed
Infrastructure as Code: Built reusable, automated CloudFormation stacks.


Scalable Design: Implemented dynamic scaling and high availability.


Monitoring & Automation: Leveraged native AWS tools for continuous monitoring and scheduled operational tasks.


Cost Optimization: Stopped instances automatically based on schedule, minimizing unnecessary spend.


Security Best Practices: Applied layered security measures throughout the solution.


##Lessons Learned
AMIs can be extended with simple User Data scripts for rapid, no-cost WordPress deployment.


You can use scaling and scheduling features in AWS to maintain solid performance at manageable cost.


Health checks are important for maintaining reliability.


##Conclusion
This project utilizes several skills and tools, including WordPress, AWS CloudFormation, and EC2 to publish a WordPress blog live, develop and test it, and ensure its security.
