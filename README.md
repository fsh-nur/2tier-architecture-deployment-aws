# 2tier-architecture-deployment-aws


## Transferring dta from our local host to AWS

### Migrating the "app" directory:

1. cd into our ssh folder where our .pem file exists

```
cd .ssh
```

2. Using the `scp` command we move the directory to aws.

```
 scp -i "tech221.pem" -r "C:\Users\fshei\Desktop\github\virtualisation\app"  ubuntu@ec2-3-252-77-70.eu-west-1.compute.amazonaws.com:/home/ubuntu/

 ```

Here we have specified the directory we would like to move first- so copy the path of the app folder, then we put our aws instance where we would like to move this folder.

How to find the instance link:

1. Navigate to your instance and select


2. Click Connect and you will find what you need to copy into your GitBash. 

