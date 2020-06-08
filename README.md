# Host a website on EC2 server

## Overview

When deciding on how to host a website that will have to a database in the long-run can be tough. AWS offers a range of  services to help you in decision making to meet your needs. Amazon EC2 (Elastic Compute Cloud) is one of most well-known services, which offers businesses the ability to run applications on the public cloud.

Developers can create instances of virtual machines and easily configure the capacity scaling of instances using the AWS console or command line interface i.e _aws-cli_.  Launching an EC2 server is like going to the store to buy a laptop to run your applications which you can access at your own convenience.

## Prerequisites

- Have an AWS account
- Create a key pair
- Create a security group, allow port 22 and 80

## Launch EC2 instance 

Sign in to the AWS console and search for “EC2”. Navigate to the EC2 dashboard and click “Launch Instance”. Do the following:

	- Choose a free-tier eligible Linux option (Amazon Linux AMI, SSD Volume Type) and click “Select”
	- Choose the option marked as free tier eligible (General Purpose — t2.micro) - it will be one of the smallest, least powerful options. Click next to configure instance details.
	- Accept default options to configure instance. 
	- Click next to add storage.
	- Add tags(optional)
	- Configure security group(choose the security group you created above)
	- Click review and launch.
	- Select existing key pair you created above.

## Provision the server

Navigate to your terminal and do the following:

### Step 1: SSH into the server

	$ chmod 400 <your keypair.pem>
	$ ssh -i "your_keypair.pem" ec2-user@ec2-user@<public_ip_from_dashboard>

Copy code from local to ec2 location on the server:

	$ scp -i /path/to/keypair/ /file/to/copy/ ec2-user@<public_ip_from_dashboard>:/home/ec2-user/

Type yes to continue

Run as root:

	$ sudo su

Update all of the packages on the instance:

	$ yum update -y 

### Step 2: Install webserver (Apache2)

	$ yum install httpd -y
	$ service httpd start
	$ chkconfig httpd on

By default, the apache web server will display the _index.html_ file found in _/var/www/html_ directory in the root path of your website then navigate to the directory

	$ cd /var/www/html 

Manually create an index.html file in this directory. Using your preferred editor _(touch, vi, nano, etc)_ create the index.html file:

	$ nano index.html

Add valid html to the file (e.g.):

	```
	<!DOCTYPE html>
	<html lang="en" >
	<head>
	  <meta charset="UTF-8">
	  <title>Hello world</title>
	</head>
	<body>
	<!-- partial:index.partial.html -->
	<div class='console-container'><span id='text'></span><div class='console-underscore' id='console'>&#95;</div></div>
	<!-- partial -->
	  <h1>Hello word</h1>
	</body>
	</html>

	```
Exit and save. Check the contents of index.html file:

	$ cat index.html 

Navigate back to AWS console copy the Public DNS(IPV4) of your instance into your clipboard. Paste the address into your browser. You should be able to see your homepage with 'Hello World' displayed!

## What's Next
The above guidelines will help you deploy your first website with ease! You can learn more [here](https://aws.amazon.com/ec2/getting-started/) 

## Conclusion
EC2 is a widely used AWS service by businesses due to its simple setup and scalability features among others. It allows users to build apps and products to automate scaling according to changing needs and peak periods. It makes it simple to deploy virtual servers and manage storage, lessening the need to invest in hardware and helping streamline development processes. What makes it more reliable and convenient is because AWS offers different instance types of EC2 for different requirements and budgets, including hourly, reserved, and spot rates. 



