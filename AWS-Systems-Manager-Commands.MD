AWS Systems Manager lets you remotely and securely manage the configuration of your managed instances. It helps you automate management tasks. 
- Create IAM Role - Assign Permissions
- Create EC2 & Assign IAM Role - "AmazonEC2RoleforSSM" role to an Amazon EC2 instance with "AmazonSSMFullAccess" Permissions
- Bootstrap with SSM
- Run Command

## User-Data:
```sh
#!/bin/bash
cd /tmp
sudo yum install -y https://s3.amazonaws.com/ec2-downloads-windows/SSMAgent/latest/linux_amd64/amazon-ssm-agent.rpm
yum install -y amazon-ssm-agent.rpm
sudo systemctl start amazon-ssm-agent
sudo systemctl enable amazon-ssm-agent
```
## Run Commands:
```sh
#/bin/bash

echo -e "{
 'Hostname':'`curl http://169.254.169.254/latest/meta-data/local-hostname --silent`', \
\n 'AMI-ID':'`curl http://169.254.169.254/latest/meta-data/ami-id --silent`', \
\n 'Kernel-Version':'`rpm -q kernel`' \
\n 'Instance Type':'`curl http://169.254.169.254/latest/meta-data/instance-type --silent`'
 }"
 ```