Step 1: Created an AWS Account (Learner Lab)
Logged into AWS Learner Lab.
Selected Asia Pacific (Sydney) region.
Accessed AWS Management Console.
Step 2: Launch EC2 Instance
Opened EC2 Dashboard.
Clicked Launch Instance.
Selected Ubuntu Server 24.04 LTS.
Selected t2.micro instance.
Created a new key pair (.pem).
Configured Security Group.

Allowed inbound rules:

SSH (22)
HTTP (80)
HTTPS (443)

Launched the EC2 instance successfully.

Step 3: Connect to EC2

Connected using EC2 Instance Connect.

Verified connection.

whoami

Output

ubuntu
Step 4: Update Ubuntu
sudo apt update
sudo apt upgrade -y
Step 5: Install Docker

Installed Docker.

sudo apt install docker.io -y

Enabled Docker.

sudo systemctl enable docker
sudo systemctl start docker

Verified Docker.

docker --version
Step 6: Install Docker Compose

Installed Docker Compose.

Verified installation.

docker compose version
Step 7: Clone GitHub Repository

Cloned project.

git clone git@github.com:BarunSharmaji/django-notes-app.git

Moved into project.

cd django-notes-app
Step 8: Verify Project Files

Verified:

Dockerfile
docker-compose.yml
nginx configuration
requirements.txt
.env
Django project files
Step 9: Configure Environment Variables

Created .env

Configured

DB_NAME=test_db

DB_USER=root

DB_PASSWORD=root

DB_HOST=db_cont

DB_PORT=3306
Step 10: Docker Compose Deployment

Started application.

docker compose up --build -d

Verified containers.

docker ps

Running Containers

Django
MySQL
Nginx
Step 11: Verify Application

Opened browser.

http://EC2-Public-IP

Verified Django Notes Application was accessible.

Step 12: Configure GitHub SSH Authentication

Generated SSH Key.

ssh-keygen -t ed25519

Added Public Key to GitHub.

Changed Git Remote to SSH.

Verified

git remote -v
Step 13: Configure GitHub Actions CI/CD

Created

.github/workflows/deploy.yml

Workflow automatically

Connects to EC2
Pulls latest code
Stops containers
Rebuilds Docker Images
Starts updated containers

GitHub Secrets Added

EC2_HOST
EC2_USER
EC2_SSH_KEY

Verified successful deployment in GitHub Actions.

Green workflow completed successfully.

Step 14: Configure IAM Role

Created IAM Role.

Attached Policy

CloudWatchAgentServerPolicy

Attached Role to EC2.

Step 15: Install CloudWatch Agent

Installed CloudWatch Agent.

sudo apt update

wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb

sudo dpkg -i amazon-cloudwatch-agent.deb
Step 16: Configure CloudWatch Agent

Executed

amazon-cloudwatch-agent-config-wizard

Configured

CPU Metrics
Memory Metrics
Disk Metrics
Log Monitoring

Saved configuration.

Step 17: Start CloudWatch Agent

Started agent.

Verified

sudo systemctl status amazon-cloudwatch-agent

Status

Active (running)
Step 18: CloudWatch Dashboard

Created Dashboard

EC2-Monitoring

Added widgets

cpu_usage_idle
disk_used_percent
disk_inodes_free

Verified graphs.

Step 19: CloudWatch Alarm

Created Alarm

HighDiskUsageAlarm

Threshold

Disk Usage > 70%

Notification

Amazon SNS Topic

EC2-Alerts
Step 20: Amazon SNS

Created SNS Topic

EC2-Alerts

Created Email Subscription.

Confirmed email subscription.

(In AWS Learner Lab, the subscription was automatically removed due to environment restrictions.)

Step 21: Trigger Alarm

Created a large test file.

dd if=/dev/zero of=testfile bs=1M count=2048

Verified Disk Usage.

df -h

Disk Usage

90%

CloudWatch Alarm changed to

IN ALARM

Verified successful monitoring.

Step 22: Load Testing using Locust

Installed Locust.

python -m pip install locust

Created

locustfile.py

Executed

python -m locust -H http://EC2-Public-IP

Opened

http://localhost:8089

Configured

Users : 50
Spawn Rate : 5

Started Load Test.

Collected

Response Time
Throughput
Request Statistics
Step 23: Security Configuration

Configured

Security Group

Allowed

SSH
HTTP
HTTPS

Configured IAM Role using least privilege.

Step 24: Final Verification

Verified

EC2 Running
Docker Containers Running
Django Application Accessible
GitHub Actions Successful
CloudWatch Dashboard Working
CloudWatch Alarm Triggered
Load Test Successful
Technologies Used
AWS EC2
Ubuntu 24.04 LTS
Docker
Docker Compose
Django
MySQL
Nginx
Git
GitHub
GitHub Actions
IAM
CloudWatch
Amazon SNS
Python
Locust
