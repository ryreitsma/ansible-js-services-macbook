# Installation
There are a few manual steps to take to install your MacBook. Do them before you run the Ansible playbook. First make sure you have enabled encryption of your filesystem! This is mandatory. After that, do the following steps:

### Create a personal access token for your Github account
You need the token to be able to install private Coolblue npm modules. See https://help.github.com/articles/creating-an-access-token-for-command-line-use/ on how to create the personal access token.

### Install XCode
This cannot be done automatically. You need to go to the Appstore, download and install XCode.
Run it and agree to the terms and services, otherwise the installation of brew modules will fail with the error:
*"msg: Agreeing to the Xcode/iOS license requires admin privileges, please re-run as root via sudo."*

### Edit the list of packages and fill in variables
The variables file ```group_vars/all/packages.yml``` contains all the packages that are going to be installed. Edit this list to your liking before running the script. Add the Github token and your Github login to ```group_vars/all/github.yml```. Last, but not least, check ```group_vars/all/main.yml``` and fill in your MacBook login.

### Install homebrew and Ansible with install.sh
Run the install.sh script to install homebrew and Ansible. You need both to run this Ansible playbook.

## Run the playbook
```
ansible-playbook playbook.yml -i hosts
```
If you have additional steps to add or want to change some setup, a pull request is always welcome!
