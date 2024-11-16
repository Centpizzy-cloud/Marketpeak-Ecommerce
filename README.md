## MarketPeak-Ecommerce Deployment on AWS EC2

** 1. Project Overview
The aim of this project was to deploy a responsive e-commerce web application (marketpeak-ecommerce) on an Amazon EC2 instance using Apache as the web server. This involved setting up the environment, managing version control with Git, configuring Apache, troubleshooting errors, and ensuring the application was live and accessible.

** 2. Steps to Deploy
2.1. Setting Up the Environment
Launch an EC2 Instance:

## Launch an EC2 instance using Amazon Linux 2 AMI.
## Configured a security group to allow:
SSH (Port 22)
HTTP (Port 80)

## Install Required Software:

# Updated the package manager:
sudo yum update -y

# Installed Apache Web Server:
sudo yum install httpd -y

# Started and enabled Apache:
sudo systemctl start httpd
sudo systemctl enable httpd

# Installed Git for version control:
sudo yum install git -y


** 2.2. Cloning the Repository
## Cloned the repository from GitHub:
git clone https://github.com/<username>/marketpeak-ecommerce.git

# Navigated into the project directory:
cd marketpeak-ecommerce

# Created a new branch for development:
git checkout -b development


** 2.3. Configuring Apache
## Copy Project Files to Apache Directory:
sudo cp -r * /var/www/html/

## Disable the Default Apache Welcome Page:

# Renamed the default welcome.conf file:
sudo mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.conf.bak

# Restarted Apache:
sudo systemctl restart httpd


** 2.4. Managing File Permissions
# Changed ownership of the project files to Apache:
sudo chown -R apache:apache /var/www/html/marketpeak-ecommerce

# Set proper file permissions:
sudo chmod -R 755 /var/www/html/marketpeak-ecommerce


** 2.5. Git Workflow
# Added all changes to the staging area:
git add .

# Committed the changes:
git commit -m "Updated HTML and CSS files"

# Set up the remote upstream branch for development:
git push --set-upstream origin development



## 3. Troubleshooting and Challenges

** 3.1. Issue: Git Authentication Failure

# Problem: Password-based Git authentication failed.
# Solution:
# Switched to token-based authentication:
# Generated a personal access token from GitHub.
# Used the token instead of a password during git push.

** 3.2. Issue: Default Apache Welcome Page
# Problem: The Apache welcome page appeared instead of the application.
# Solution:
# Renamed the welcome.conf file and restarted Apache:
sudo mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.conf.bak
sudo systemctl restart httpd


** 3.3. Issue: Permission Denied on File Merge
# Problem: Encountered Permission denied errors while merging branches or switching to main:
error: unable to unlink old '2128_tween_agency/css/tooplate-tween-agency.css': Permission denied
# Solution:
# Fixed by adjusting permissions:
sudo chown -R ec2-user:ec2-user /var/www/html/marketpeak-ecommerce

** 3.4. Issue: Merge Conflict
# Problem: Could not merge development into main due to uncommitted changes:
# Please commit your changes or stash them before you merge.
git stash
git merge development
git stash pop

## 4. Verification
# Accessed the deployed application in the browser using the public IP of the EC2 instance
http://<EC2_PUBLIC_IP>

## 5. Conclusion
This project demonstrated the successful deployment of a web application on an AWS EC2 instance. It required configuring Apache, troubleshooting errors, and managing Git workflows. Through this project, I gained hands-on experience in deployment and resolved challenges such as Git authentication, file permissions, and merge conflicts.

