
# CAPSTONE PROJECT: INTRODUCTION TO CLOUD COMPUTING

#### 1. Created project directory and initialize a Git repository.
I begin by creating a project directory named "MarketPeak_Ecommerce" and initialize a Git repository to manage the version control.
```bash
mkdir MarketPeak_Ecommerce
cd MarketPeak_Ecommerce
git init
```
#### 2. Downloaded E-commerce website and extracted
I download the free e-commerce website and extract the downloaded template into my project directory `MarketPeak_Ecommerce`

#### 3. Stage and Commit the Template to Git
I staged the extracted website template into my git repository by running the command. And check the status
```bash
git add .
git status
```
#### 4. Set git global configuration with my username and email
```bash
git config --global user.name "nomolos98" git config --global user.email "nomolos98@gmail.com" git commit -m "Initial commit for MarketPeak e-commerce site"
```
#### 5. Push the Code to GitHub Repository
- I log into my GitHub account and create a new repository named "MarketPeak_Ecommerce". I Leave the repository empty without initializing it with a README, .gitignore, or license.
- Within my project directory, i add the remote repository URL to my local repository configuration
```bash
git remote add origin https://github.com/nomolos98/MarketPeak_Ecommerce.git
```
I push my local repository content into GitHub
`git push -u origin main`

### AWS Deployment
#### 1. Set Up an AWS EC2 Instance
I log in to the AWS Management Console, Launch an EC2 instance using an Amazon Linux AMI and Connect to the instance using SSH.
#### 2. Authenticating my GitHub by cloning the repository with ssh
- I generated SSH keypair using "ssh-keygen"
Type `ssh-keygen` in my prompt. it generated the key pair and added the SSH public key to my GitHub account.
- I cloned the repository by running "git@github.com:nomolos98/MarketPeak_Ecommerce.git"

#### 3. Install a Web Server on EC2
I installed a Apache webserver on my EC2 by running the commands:  
```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```
I configure httpd for Website, by clearing the default httpd web directory using `sudo rm` and copy MarketPeak E-commerce website files to it using `sudo cp`.
```bash
sudo rm -rf /var/www/html/*
sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/
```
I applied the changes by reloading the httpd server by running the command
`sudo systemctl reload httpd`
I opened my web browser and access the IP of my EC2 to view the deployed website

### Continuous Integration and Deployment Workflow
###### 1. For the New Features and Fixes, created Development Branch
```bash
git branch development
git checkout development
```
###### 2. I stage, commit and push changes to GitHub
```bash
git add .
git commit -m "Add new features or fix bugs"
git push origin development
```
###### 3. On my GitHub, i created a pull request, review and merged the development branch with the main branch and Push the Merged Changes to GitHub; I switched to the main branch by running the command "git checkout main"
```bash
git checkout main
git merge development
git push origin main
```
###### 4. I navigated to the production server where the production website is hosted and pull the latest changes from the main branch by running the command "git pull origin main"
```bash
git pull origin main
sudo systemctl reload httpd (Restart the Web Server if necessary)
```
###### 5. Test the new changes. open a web browser and navigate to the public IP address of your EC2 instance
