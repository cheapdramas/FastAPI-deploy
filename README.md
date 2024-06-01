### This is simple example for deploying your FastAPI application, to production environment without any investment. HTTPS protocol +

### We need:

-Account on Amazon Web Services
-EC2 instance
-FastAPI app

### Account on AWS

You need to create new AWS account. Visit https://portal.aws.amazon.com/billing/signup#/start/email 


### EC2 Instance
At this stage, i hope you have created AWS account successfully


At the main page | Console Home press ALT + S or find Search tab at the top. Look for EC2
![](/src/ec2_search.jpg)

Click on the first result. Now what you should see is this page:
![](/src/ec2_main.jpg)

Find "Instances" tab in the left menu. Now what you should see is this page:
![](/src/ec2_instances.jpg)

Click "Launch Instances" at the right top of page. Now you are launching a new EC2 instance.
1.Pick a name for your instance
2.For "Application and OS Images (Amazon Machine Image)" choose Ubuntu.
3.For "Instance type" choose t3.micro cause it`s free
4.For "Key pair (login)" press "Create new key pair". Enter key pair name, for "Key pair type" choose RSA, for "Private key file format" choose .pem. Click "Create key pair"
![](/src/key_pair.jpg)

Now, when you created a new key pair, click refresh button and choose your key pair.
![](/src/key_pair_final.jpg)

5.For "Network settings" set everything like this:
![](/src/network_settings.jpg)
6.You can ignore 2 last stages and click "Launch instance"


### Connect to your EC2 instance

Now, when you have created your ec2 instance, you should see this page:
![](/src/connect_1.jpg)

Choose connect to your instance.

If you cant find this page, dont worry, on the left menu click "Instances", click at your Instance ID.You should see this page:
![](/src/connect_2.jpg)

Now, click "Connect"
![](/src/connect.jpg)
Click "Connect"

Ok, so now what you should see is a linux terminal that represent our server.
![](/src/terminal.jpg)

