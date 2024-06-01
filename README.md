### This is simple example for deploying your FastAPI application, to production environment without any investment. HTTPS protocol encluded

### We need:

- Account on Amazon Web Services
- EC2 instance
- FastAPI app

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
- 1.Pick a name for your instance
- 2.For "Application and OS Images (Amazon Machine Image)" choose Ubuntu.
- 3.For "Instance type" choose t3.micro cause it`s free
- 4.For "Key pair (login)" press "Create new key pair". Enter key pair name, for "Key pair type" choose RSA, for "Private key file format" choose .pem. Click "Create key pair"
![](/src/key_pair.jpg)

Now, when you created a new key pair, click refresh button and choose your key pair.
![](/src/key_pair_final.jpg)

- 5.For "Network settings" set everything like this:
![](/src/network_settings.jpg)
- 6.You can ignore 2 last stages and click "Launch instance"


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

### Creating FastAPI service

- 1 . `git clone <Your repository link>`
- 2 . `cd <Your repository name>`
- 3 . IF you have requirements follow by 5,6,7 steps, if you're not, ignore them
- 4 . `sudo apt update`
- 5 . `sudo apt install python3-pip`
- 6 . press y then enter
- 7 . `sudo pip install -r requirements.txt --break-system-packages`
- 8 . `cd ..` 
- 9 . `sudo pip install gunicorn --break-system-packages`
- 10 . `sudo nano /etc/systemd/system/fastapi.service` and paste block code below and change text in <> to your variables

```

[Unit]
Description=fastapi service
After=network.target

[Service]
User=ubuntu
Group=www-data
WorkingDirectory=/home/ubuntu/<YOUR REPOSITORY NAME>
ExecStart=gunicorn <NAME OF YOUR MAIN FILE>:<FASTAPI CLASS OBJECT> --workers 4 --worker-class uvicorn.workers.UvicornWorker --bind 0.0.0.0:8000

Restart=always

[Install]
WantedBy=multi-user.target

```

Hit "Ctrl+X" then "Y" for save the "fastapi.service" (For Nano editor)

Now our FastAPI application more robust and easy to control. For start and enable the service, run:

` sudo systemctl start  fastapi`

To enable the service:

` sudo systemctl enable  fastapi`

To stop the service:

` sudo systemctl stop  fastapi`

To see status of the service:


` sudo systemctl status  fastapi`


- Last step is for activate service: `sudo systemctl start  fastapi` then ` sudo systemctl enable  fastapi`



### Caddy
Caddy will help us with https protocol.

## Installation:
- `sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https`


- `curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg`

- `curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list`

- `sudo apt update`

- `sudo apt install caddy`







