# 2tier-architecture-deployment-aws


## Transferring data from our local host to AWS

### Migrating the "app" and "db" directory:

## Use the same steps respectively  the "environemt" folder in our local host.

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


|App Instance |DB Instance|
|-----------|-----------|
