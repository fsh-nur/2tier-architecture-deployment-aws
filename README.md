
 ## Autoscaling

AutoScaling in AWS is the advanced cloud computing feature that provides **automatic resource management** based on the server’s load. E.g when deploying instances, if one data centre went down it will go to another one
autoscaler replaces and terminates the instances.

## Load Balancing

Load balancing is the process of distributing a set of tasks over a set of resources (EC2 Instances),  with the aim of making their overall processing more efficient. Until there is a status 200 recieved from an autoscaler, it will divert traffic traffic.


![Screenshot_1](https://user-images.githubusercontent.com/129324316/234581569-28e4c14f-0db0-4bf3-a4ef-ebf38c27613e.png)

*Application Load Balancer is the most efficient load balancer: application load balancer works on the 7th layer — application layer — in the OSI model. Made for cloud environments, application load balancers assess application content and routes it to applications in the AWS public cloud.*

## Scaling Up vs Scaling Out

- Scale up (bigger server)
- Scale out (replicas of the same size)   (*Load balancing follows a scale out structure*)

## High Availability in AWS

- High availability means that a system will almost always maintain uptime, albeit sometimes in a degraded state. With regard to AWS, a system has high availability when it has 99.999% uptime, also known as "five nines". To put that in perspective, the system would be down for a mere five minutes and fifteen seconds a year.
 

## What we need:
 
- Create a template with the required information in order to deploy an internet facing app available on port 80
- In order to test it- installing nginx with the help of autoscaling group this is replicated to all the instances

 
## Steps
 

1. Create a lanch template
2. Naming Convention
3. Use 18.04 Ubuntu ami (18.04 LTS, amd64 bionic image build on 2022-09-01)
4. Instance Type t2.micro
5. Key-pair tech221
6. Selecting exzisting group in entwork configuration port 80 should be available.
7. Advanced Network settings: #!/bin/bash
sudo apt update && sudo apt upgrade -y
sudo apt install nginx -y
8. Create template
9. auto scaling group
10. Select our template
11. Choose Launch Instance options
12. Select VPC
13. Choose availablity zones(multiple eg. ey-west1a, b, c)
14. Instance type requirements according to template
15. Attach to a new load balancer
16. Application load balancer select
16. Select internet facing
17. Default VPC selected 
18. These are the subnets we would like to balance the load on
19. Who can get to the load balancer
20. You can create a target group 
21. Health checks determine whether traffic is sent or diverted for 300 seconds before it determines whether the threshold of CPU utilisation is above 50%. If it is below 50% it will not spin up new instances. Turn on health checks.
22. Configure group size and scaling policies depending on what is the reason of your scaling policy.
23. There are many reasons to monitor the health of our instances such as the netowork (how many people are accessing) as well as CPU utilisation
24. Make percentage 50 
25. Configure the amount of seconds of grace given before a new instance is made
26. Add notifications during production
27. Add tags that can be attached to all the large resources we are creating
28. Naming config: name/group/asg/alb/app
29. Now entering the review page
30. Create an autoscaling group- the capacity and zone they are in.
31. Instances are being run in multiple availabilty zones and is distributed with a load balancer 
32. Now we test the load balancer and the autoscaling group
33. Ways to test: Increasing CPU above 50% threshold and seeing if a new instance is created
Deleting an instance purpposefully and observing if a a new instance 
34. Terminate an instance in one availability zone
35. A new one should be intialised with a different ip and you can determine which one is yours when you look at the security groups 


