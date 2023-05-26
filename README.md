
# ODOO v16
A Simple base odoo development project
<br/><br/>

# Installation
With Docker and Docker-Compose

### Set up the repository (Ubuntu based OS)
```sh
# Update the apt package index and install packages to allow apt to use a repository over HTTPS:
$ sudo apt-get update
$ sudo apt-get install ca-certificates curl gnupg

# Add Docker’s official GPG key:
$ sudo install -m 0755 -d /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
$ sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Use the following command to set up the repository:
$ echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
<br/>

### Install Docker Engine (Ubuntu based OS)

```sh
# Update the apt package index:
$ sudo apt-get update

# Install Docker Engine, containerd, and Docker Compose.
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
<br/>

### Setup Odoo

```sh
# change the setting on etc/odoo.conf to your database setting
$ nano ./etc/odoo.conf

# run the docker-compose script
$ docker-compose up -d

# login with this credential
access: http://localhost:10016/
username: admin
password: admin

* dont forget to change the password as soon as you logged in!
```
<br/><br/>

# Getting Started
This section will guide you to create new addon and more

### How to change password
```
> After logged in click the your profile section (top right corner)
> click on myprofile
> click on action (gear icon)
> click on change password
```

### How to see logs
```sh
# for see existing logs in 10 lines
$ tail -n 10 ./etc/odoo-server.log 

# for monitoring logs
$ tail -f -n 0 ./etc/odoo-server.log 
```

### Create new addon
```sh
# Create new addon with scaffolding
$ docker-compose exec odoo16 odoo scaffold <addon_name> /mnt/extra-addons

# Change ownership from root to current user (to allow edit files)
$ sudo chown $(id -u):$(id -g) -R ./addons

# Activate the developer option
- go to the home menu (top left icon) and choose `Settings`
- on `Developer Tools` section choose `Activate the developer mode`

# Activate selected Addon
- go to the home menu (top left icon) again and choose `Apps`
- click on `Update Apps List` then click update
- Deselect the apps filter and type your module name on search bar
- click on `activate`

# Code your addon
- use your code editor to edit the addon located on `./addons/<your addon name>`
- then go to the home menu (top left icon) again and choose `Apps`
- find your addon, click the 3 dots, and click upgrade

# run the addon model
$ docker-compose restart odoo16
```
