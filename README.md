# EC2 Setup Script Deployment

This repository provides instructions for securely transferring a `setup.sh` script from a local Windows machine to an AWS EC2 instance using SCP and a PEM key.

## Prerequisites

- An AWS EC2 instance with a public IP address
- A `.pem` key file (downloaded during EC2 instance launch)
- OpenSSH and PowerShell available on your Windows system
- SCP command-line tool (available via Git Bash or Windows 10+)

## Step 1: Set Permissions on the PEM File

Windows requires the `.pem` file to have restricted permissions for security. Run the following commands in **Command Prompt** (not PowerShell):

```cmd
powershell -Command "& {icacls '<path-to-pem-file>.pem' /inheritance:r}"
for /f "delims=" %u in ('whoami') do powershell -Command "icacls '<path-to-pem-file>.pem' /grant:r '%u:(R)'" 
```

##🔁 Replace <path-to-pem-file> with the full absolute path to your PEM file. Example:

```cmd
C:\Users\YourUsername\.ssh\my-key.pem
```

## Step 2: Transfer the Setup Script to EC2 Using SCP

```cmd
scp -i "<path-to-pem-file>.pem" <local-path-to-setup.sh> ec2-user@<ec2-public-ip>:/home/ec2-user/
```
Replace:

<path-to-pem-file>.pem> → Your PEM key path.

<local-path-to-setup.sh> → Path to your setup.sh script (e.g., X:/scripts/setup.sh).

<ec2-public-ip> → The public IP of your EC2 instance.




