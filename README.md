# TRYHACKME-AZURETAPPER
Azure defender practices

Recently explore the machine and gain access on it to discover Custom Script which has been protected and encrypted to get the flag.

General info:
 - A general read user to login to Azure which I can play around to see the environment I am in.
 - A password: D3l4w4r3R1v3r$#@!.
 - That don't know who I can gain access to and which access we have for that.

START THE EXPLORATION ...

Which we need for this lab: 

- CLI with az module on any machine so we can bypass the MFA which we don't want to interract with.
IF NOT, we can try to install based on your own OS is using for this lab:

Linux: [Microsoft]https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?view=azure-cli-latest&pivots=apt .
- Or following below process:

1. Get packages needed for the installation process:
   
   `sudo apt-get update`
   `sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release`
   
2. Download and install the Microsoft signing key:
   
   `sudo mkdir -p /etc/apt/keyrings`
   ```
   curl -sLS https://packages.microsoft.com/keys/microsoft.asc |
   gpg --dearmor | sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null
   sudo chmod go+r /etc/apt/keyrings/microsoft.gpg
   ```
   
3. Add the Azure CLI software repository:
   ```
   AZ_DIST=$(lsb_release -cs)
   echo "Types: deb
   URIs: https://packages.microsoft.com/repos/azure-cli/
   Suites: ${AZ_DIST}
   Components: main
   Architectures: $(dpkg --print-architecture)
   Signed-by: /etc/apt/keyrings/microsoft.gpg" | sudo tee /etc/apt/sources.list.d/azure-cli.sources```
   
4. Update repository information and install the azure-cli package:
   `sudo apt-get update`
   `sudo apt-get install azure-cli`

And the NOTE to take note all info which you will use later.

How to read all file in order to understand the process:
 -First start with user which is provide by the lab: InfoNote.md
 -After recon, we will start to gain the access to Gumby in order to get accesses needed for accessing VM (Goo, Pokey): Walkthrough.md
 -Login to each account with TAP:
    +Work with VM: Pokey.md
    +Work with VM network for ssh connection: Goo.md

