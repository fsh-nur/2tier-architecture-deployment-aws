# Why do you need to monitor?

- The primary goal of monitoring AWS is to ensure your infrastructure and applications work as expected at all times.
- Ultimately, monitoring your AWS environments can help you find out what you need to improve to maximize ROI, performance, and costs.

# 4 Golden rules of Monitoring

-Latency
-Traffic 
-Errors
-Saturation. 

# What is Alert Management

- Alert management generally occurs within IT or operations departments and provides them the ability to be able to be notified and aware of current or potential upcoming issues with how their services and systems are functioning.

# SNS simple notification service

- Amazon Web Services Simple Notification Service (AWS SNS) is a web service that automates the process of sending notifications to the subscribers attached to it. 
- SNS provides this service to both application-to-person and application-to-application. 
- It uses the publishers/subscribers paradigm for the push and delivery of messages. 
- The data loss is prevented by storing the data across multiple availability zones. 
- It is cost-efficient and provides low-cost infrastructure, especially to mobile users.

# SQS Simple Queue service

- Simple Queue Service (SQS) is a service provided by AWS that allows you to exchange and store messages between software components.
- It is a fully managed message queuing service that helps you to decouple and scale microservices, distributed systems, and serverless applications. 
- You can send messages to an SQS queue and pull them from the queue based on your capacity and discretion.


# Cloud watch to monitor AWS service/s

- Amazon CloudWatch monitors your Amazon Web Services (AWS) resources and the applications you run on AWS in real time. 
- You can use CloudWatch to collect and track metrics, which are variables you can measure for your resources and applications.
- You can create alarms that watch metrics and send notifications or automatically make changes to the resources you are monitoring when a threshold is breached. For example, you can monitor the CPU usage and disk reads and writes of your Amazon EC2 instances and then use that data to determine whether you should launch additional instances to handle increased load. You can also use this data to stop under-used instances to save money.
