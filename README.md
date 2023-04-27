# 2tier-architecture-deployment-aws


## Transferring data from our local host to AWS

### Migrating the "app" and "db" directory:

## Use the same steps respectively  the "environment" folder in our local host.

1. cd into our ssh folder where our .pem file exists

```
cd .ssh
```

2. Using the `scp` command we move the directory to aws.

```
 scp -i "tech221.pem" -r "C:\Users\fshei\Desktop\github\virtualisation\app"  ubuntu@ec2-3-252-77-70.eu-west-1.compute.amazonaws.com:/home/ubuntu/

 ```

Here we have specified the directory we would like to move first- so copy the path of the app folder, then we put our aws instance where we would like to move this folder.

How to link the instance:

1. Navigate to your instance and select

![finding link connect instance](https://user-images.githubusercontent.com/129324316/233976952-c0384cc6-eddc-41e8-99aa-a83ba4d994d3.png)



2. Click Connect and you will find what you need to copy into your GitBash. 




![link2instance](https://user-images.githubusercontent.com/129324316/233976963-7df0530a-6b3f-4bb0-a906-d5534730a308.png)


## Deploying the app on aws

1. Making sure that port 3000 is open where the app is hosted:
  - Navigate to your Security Group
  - Edit Inbound Rules 
  - Create a rule allowing port 3000
 
 2. SSH into your instance in the ssh folder paste this in highlight.
 
 
 ![link2instance](https://user-images.githubusercontent.com/129324316/234017469-f0ae8b99-e71f-4cd4-a35e-69b6420be739.png)

3. Install  packages running these commands:

```

sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install nginx -y
sudo systemctl start nginx
sudo systemctl enable
sudo apt-get install python -y
# install nodejs
sudo apt-get install python-software-properties
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install nodejs -y

# install pm2
sudo npm install pm2 -g


```
 
 
4. In Gitbash deploy the app after navigating to the app folder
 
 ```
 cd app
 node app.js
 ```
 
5. When pasting your IP in the browser you should see the following pages:


![app](https://user-images.githubusercontent.com/129324316/234064946-3055a480-a1e6-4df2-8415-0360d3a0cbed.png)


![fib](https://user-images.githubusercontent.com/129324316/234064973-67dcd03c-a787-4f72-8157-5afef8db83f3.png)


## Reverse Proxy

1. Navigate to the folder holding the config files for nginx 
```
cd /etc/nginx/sites-available
```

2. Create a new configuration file with nano by using the following command:

```
sudo nano nodeapp.conf

```

3. Enter the following into the file:

```
server {
   listen 80;
   server_name -ip_address-;

   location / {
       proxy_pass http://-ip address-:3000;
       proxy_set_header Host $host;
       proxy_set_header X-Real-IP $remote_addr;
       proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       proxy_set_header X-Forwarded-Proto $scheme;
   }
}
```
Ofcourse, use CTR + X and y to save

4. Enter this command 
```
sudo ln -s /etc/nginx/sites-available/nodeapp.conf /etc/nginx/sites-enabled/nodeapp.conf

```
5. Check for any errors in the config file:
```
 sudo nginx -t

```
6. Reload nginx

```
sudo systemctl reload nginx

```
7. Enable nginx
```
sudo systemctl enable nginx

```
8. Now navigate to the app and run it

```
cd app

node app.js
```
9. If you want to kill the previous running of the app enter
```
lsof -i tcp:3000

kill -9 PID

```
10. Now your app will run, without needing to specify the port number.

![reversre](https://user-images.githubusercontent.com/129324316/234068961-42e4ab2d-530c-4300-a7f4-c13f85a5ac33.png)

## Creating a Database server and moving MongoDB to the cloud

1. Create a new EC2 Instance on AWS and name it 
2. Make sure to select ubuntu 18.04 which can be found by searching **ami-07b63aa1cfd3bc3a5**
3. Edit your security group and input the following options:

![creating db server](https://user-images.githubusercontent.com/129324316/234069988-727ee3d3-718b-4ec9-8337-b2f36d38e7de.png)

4. Launch the instance
5. SSH into the instance in GitBash
6. In order to install mongodb you must enter the following commands individually:

```
sudo apt update -y 

sudo apt upgrade -y

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv D68FA50FEA312927

echo "deb https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list

sudo apt update -y 

sudo apt upgrade -y

sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20

sudo systemctl start mongod
```

## Connecting the app and database instances


|DB Instance |App Instance|
|-----------|-----------|
|1. cd to home folder:  ```cd app```|8. ```cd ```|
|2. open mongod configuration file:  ```sudo nano /etc/mongod.conf```|9. sudo nano .bashrc - open .bashrc file to create your environment variable there |
|3. Scroll down, change bindip to 0.0.0.0|10. Scroll to the bottom and write export DB_HOST=mongodb://<ip>:27017/posts |
|4. CTRL + X and y to save|11. ```source .bashrc``` restarts .bashrc file to apply changes|
|5. Restart mongod :```sudo systemctl restart mongod```|12. ```cd app```|
|6. Enable autostart of mongo: ```sudo systemctl enable mongod```|13. ```node seeds/seed.js``` - seed data to database|
|7. Ensure that mongo is running: ```sudo systemctl status mongod ```|14. Run the app by using node app.js and search your IP/posts in your web browser|
 
 
 The following page should appear:
 
 ![posts](https://user-images.githubusercontent.com/129324316/234239523-7dc09a3a-ab11-4342-9b75-0bfffe26f897.png)
 
 ==========================================================================================================================
 
 
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


