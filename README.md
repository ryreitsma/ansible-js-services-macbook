# Why should I use this script to install my Macbook?

I created this script because I don't like repetitive tasks, especially if they can be easily automated. Also, I tend to forget things, so if I needed to reinstall, I would get stuck on simple configuration steps. This is why I created this script. Anyone in Coolblue can now use this script to do the most common setup steps. You'll see that installing a Macbook still requires some manual steps, just follow this readme and you can get going rather quickly. 

Having trouble installing? Missing some setup or configuration? Please let me know via Hangouts, a Github issue or walk by my team's room. I'd be glad to help out. 

# Installation
There are a few manual steps to take to install your MacBook. Do them before you run the Ansible playbook. First make sure you have enabled encryption of your filesystem! This is mandatory. After that, do the following steps:

### Create a SSH key and add it to your Github account
To be able to clone repositories, you need to have an SSH key installed on the MacBook which has been added to your Github account. See https://help.github.com/articles/generating-ssh-keys/ on how to do this.

### Create a personal access token for your Github account
You need the token to be able to install private Coolblue npm modules. See https://help.github.com/articles/creating-an-access-token-for-command-line-use/ on how to create the personal access token.

### Clone this repository
Validate that your ssh key is working by cloning this repository with ssh:

```git clone git@github.com:ryreitsma/ansible-js-services-macbook.git```

### Install XCode
This cannot be done automatically. You need to go to the Appstore (you can find the Appstore in the bottombar of the Macbook), download and install XCode.
Run it and agree to the terms and services, otherwise the installation of brew modules will fail with the error:
*"msg: Agreeing to the Xcode/iOS license requires admin privileges, please re-run as root via sudo."*

### Edit the list of packages and fill in variables
There are a few files which contain variables you need to edit to allow the install to run succesfully. Also, you can edit to install the things you need. The file ```group_vars/all/packages.yml``` contains all the packages that are going to be installed. Edit this list to your liking before running the script. Add the Github token and your Github login to ```group_vars/all/github.yml```. This is also where you can specify which repositories the script should clone and add to your MacBook. NOTE: you can only install repositories you've already forked from coolblue-development!

Last, but not least, check ```group_vars/all/main.yml``` and fill in your MacBook login / username.

### Install homebrew and Ansible with install.sh
Run the install.sh script to install homebrew and Ansible. You need both to run this Ansible playbook.

## Run the playbook
Some of the install steps in the playbook.yml file are optional. If you don't want to install atom, just comment out or  remove the role for software/atom.
```
ansible-playbook playbook.yml -i hosts
```
If you have additional steps to add or want to change some setup, a pull request is always welcome!

#### FAQ

* How can I use Oracle sqldeveloper on my Macbook?

Download it from here http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html. Double click to run it. Then click on 'Oracle SQL Developer' in the top bar, select Preferences -> Database -> Advanced. You will see a Tnsnames Directory input box. Enter /Users/{{ your Macbook login / username }}/Oracle/instantclient, that is where the tnsnames.ora file was added. From now on, if you want to connect to an Oracle database, you can use the TNS option to get the correct connection properties.

* I get a lot of errors when running the 'Add Coolblue upstream to repositories' task

If you see 'stderr: fatal: remote upstream already exists....ignoring' then don't worry, it just indicates that the upstream already exists. This is a known bug. 
