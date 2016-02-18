# upalatedeploy
Deployment stuff for the Upalate team 

## Steps

	sudo vagrant plugin install vagrant-cahier

	sudo vagrant plugin install vagrant-hostmanager

	vagrant up

The `vagrant-cachier` plugin will speed up the `vagrant up` process.
The `vagrant-hostmanager` plugin is not strictly needed as of now, but
will be useful as we add more boxes.

### Ancillary Commands

 To see the current status of the machine, `vagrant status`

SSH to the machine with `vagrant ssh`

