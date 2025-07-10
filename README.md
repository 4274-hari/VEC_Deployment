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
