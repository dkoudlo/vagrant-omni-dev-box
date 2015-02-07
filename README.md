# vagrant-omni-dev-box
Vagrant Box for Web Development

## Install 
Download Install Vagrant + VirtualBox

-Docker in future-

After Install Open Terminal and run

vagrant box add ubuntu/trusty64

vagrant plugin install vagrant-omnibus

vagrant up # the only thing to do (need to check if still adding the box is necessary on very initial setup)

# Now ssh into the machine
vagrant ssh

# if you are getting ssh -command not found make sure openssh installed in cygwin (aka run 'ssh' in terminal from which vagrant command is ran)


# Shared Directory 
```/vagrant``` -> mapped to the directory you are in workspace workspace/galaxy-swager

## Stopping vm
```vagrant suspend``` # run freeze/pause vagrant
```vagrant halt``` # gracefull shutdown of vm
```vagrant detroy``` # will remove all tracec

# PROVISIONING
if running and updated provision
```vagrant reload --provision```
or
```vagrant destroy``` # detroy the vm
```vagrant up``` # reprovision everything from clean vm