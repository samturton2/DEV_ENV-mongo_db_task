# Mongo DB Dev Env Task

## Summary

The developers have indicated that they'll need a mongodb database soon. We need to create a provisioning script that will create this server.
#### Acceptance criteria
- Uses vagrant file
- Create VM and MongoDB is working
- MongoDB 3.2.20 is installed

## Instructions
These instructions will take you through how to setup and run this virtual environment with MongoDB 3.2.20 installed. Please complete the prequisites first and complete the tasks in order.

## Prerequisites
- Click on the below repo, and follow the steps to downloading Ruby, then vagrant, then virtual box. Ignoring step 4 for now.
  -  https://github.com/khanmaster/vb_vagrant_installtion

- Once all 3 programmes are installed clone this repo on your device.
    - copy the url link of this repo
    - Open your bash terminal as admin
    - In the directory you want the repo follow these commands
    - `git init`
    - `git clone <pasted link>`

# Main Commands
- First check if there is a .vagrant/ file in the repo using
```bash
ls -a
```
- Run command to initiate vagrant in the repo if no .vagrant file is found
```bash
vagrant init
```

- Run this command for a list of your installed plugins
```bash
vagrant plugin list
```

- If it shows `vagrant-hostsupdater` you can move on
- If not: install the plugin using this command
```bash
vagrant plugin install vagrant-hostsupdater
```
- For more information on this plug in view https://github.com/agiledivider/vagrant-hostsupdater or scroll to the extra commands section of this documentation.

- Run this command to start runnning the Virtual Machine
```bash
vagrant up
```

- Run this command to enter the running virtual environment
```bash
 vagrant ssh
```

- Test the DB to make sure everything runs

#### Behind the scenes
- Vagrant up should run the the provision.sh file in the environment/db directory
- In this file we can see all shell commands to install the packages necessary 
- for running a MongoDB in the virtual machine
- If you open the vagrant file in the main directory, you should see the `config.vm.provision` command (line 17)  telling the programme to run the provision installation commands once the virtual environment is up and running.
- In the vagrant file, notice the line which syncs a config folder to the VM. This folder has a copy of the mongo config file with the bing IP address changed manually to 0.0.0.0. In the provision file (before the mongodb is started), it commands the vm to copy and replace the config file with my manually edited one, so the IP address is changed accordingly.

## Testing the Virtual Environment
- Open a new terminal whilst the virtual environment is still running.
- `cd` into the directory of the `Gemfile` and `Rakefile` which should be in the `spec-tests` folder. e.g  `cd ./environment/spec-tests`

- Run this command to test the environment has all the packages needed
```bash
rake spec
```

- All the tests should pass if mongodb is running in the correct place