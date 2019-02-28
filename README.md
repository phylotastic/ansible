# ansible

First install ansible in the controller. The easy way:

```
sudo easy_install pip
sudo pip install ansible
```

The whole following chunk comes from @bomeara's repo
I'm juts copy pasting here so we can modify it later


install ansible on the controller (lab18)

Then install ansible. For macs:

```
curl https://bootstrap.pypa.io/get-pip.py > ~/Downloads/get-pip.py
sudo python ~/Downloads/get-pip.py
sudo pip install ansible
```

```
sudo mkdir /etc/ansible/
```

copy the hosts to /etc/ansible/hosts

`sudo cp hosts /etc/ansible/hosts`

copy the R role:

`ansible-galaxy install oefenweb.r`

R shiny:

`ansible-galaxy install oefenweb.shiny-server`

Docker

`ansible-galaxy install geerlingguy.docker`

## for workers, install ubuntu 18.04. Then `sudo apt install openssh-server`. Then `sudo apt install python2.7 python-pip`


## copy your ssh key to each host (for macs or linux


```
ssh-copy-id bomeara@omearaclusterf.nomad.utk.edu
ssh-copy-id bomeara@omearaclusterk.nomad.utk.edu
```


and so forth

Make sure everything is working:

```
 ansible all -m ping
 ```

playbooks are in the playbooks dir. (note -K and --ask-become-pass do the same thing)

update packages:

`ansible-playbook -K updateapt.yml`

If you want to update ubuntu and restart

`ansible-playbook -K update_and_reboot.yml`

If you want to update ubuntu and restart on one computer only,

`ansible-playbook -K update_and_reboot_ask_for_host.yml`

and it will ask you which host. Good for setting up a new host

If you want to install R and dependencies

`ansible-playbook installR.yml --ask-become-pass`

It'll ask you for your password to install R as sudo, then install on linux hosts

To add new R packages, add them to installR.yml. You can add packages from github or from CRAN: see examples below `r_packages`. Remember to add `type: github` for github ones

If you need to clobber R to reinstall,

`ansible-playbook removeR.yml --ask-become-pass`

For the head node (omearalab13.nomad.utk.edu) do

`ansible-playbook updateserver.yml --ask-become-pass`

to set it up.

Adding slurm:

`ansible-playbook install_slurm.yml --ask-become-pass`
