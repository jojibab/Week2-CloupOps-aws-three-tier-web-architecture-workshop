# MERN Stack Application on AWS Three Tier Web Architecture 

## Description: 
This is a hands-on walk through of a three-tier web architecture in AWS. I manually created the necessary network, security, app, and database components and configurations in order to run this architecture in an available and scalable manner.

### Tech Stack Used 
* React
* Nodejs
* MySQL
* AWS Services (VPC, EC2, RDS, S3, ELB, ASG, Cloudfront, IGW, NAT GW, Route53, ACM).  

## Pre-requisites:
1. An AWS account. If you don’t have an AWS account, follow the instructions [here](https://aws.amazon.com/console/) and
click on “Create an AWS Account” button in the top right corner to create one.
1. IDE or text editor of your choice.

## Architecture Overview
![Architecture Diagram](https://github.com/aws-samples/aws-three-tier-web-architecture-workshop/blob/main/application-code/web-tier/src/assets/3TierArch.png)

## My Three(3) Tier Architecture Diagram
![Architecture](./images/Architectural%20Diagram-final.jpg)

In this architecture, a public-facing Application Load Balancer forwards client traffic to our web tier EC2 instances. The web tier is running Nginx webservers that are configured to serve a React.js website and redirects our API calls to the application tier’s internal facing load balancer. The internal facing load balancer then forwards that traffic to the application tier, which is written in Node.js. The application tier manipulates data in an Aurora MySQL multi-AZ database and returns it to our web tier. Load balancing, health checks and autoscaling groups are created at each layer to maintain the availability of this architecture.

The frontend code is located in web-tier directory inside the application-code folder.

The backend code is located in app-tier directory inside the application-code folder.


## 🖥️ ️Installation of backend

Now we need to modify the DbConfig.js file that holds all the configuration details of the database. It should be in the app-tier directory.

     cd application-code/app-tier
     vim DbConfig.js
Add below content, Replace the values in string with your RDS credentials

    DB_HOST='localhost or RDS_URL'
    DB_USER='MSQL RDS Username'
    DB_PWD='Passwod of RDS'
    DB_DATABSE='Database name' 

Note: You should have nodejs installed on your system. Node.js
👉 let install dependency to run Nodejs API


    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash 
    Source ~/.bashrc
* Next, install a compatible version of Node.js and make sure it’s being used:

        nvm install 16 
        nvm use 16

* Install npm and start the backend server using pm2, pm2 a daemon process manager that will keep our node.js app running even after we exit the instance or if it is rebooted:

        cd application-code/app-tier
        npm install
        pm2 start index.js
        pm2 list

If you see “errored,” you’ll need to troubleshoot. To check the latest errors, use this command:

    pm2 logs

Note: If you encounter any issues, check your configuration file for typos and ensure you’ve followed all installation commands correctly.

    To ensure the app starts and keeps running after server interruptions or reboot, run the following command and save the current list of node processes:

    pm2 startup 
    pm2 save

Check endpoint

    curl http://localhost:4000/health

Next, test your database connection by hitting the following endpoint locally: Replace Database-name with the name of your database

    curl http://localhost:4000/Database-name


## 🖥️ Installation of frontend
Navigate to the web-tier directory

    cd application-code/web-tier
    npm install
    npm run build
