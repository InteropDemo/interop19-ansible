## Setup Ansible Docker

[Interop19-Docker/Ansible](https://github.com/InteropDemo/interop19-docker/tree/origin/master/ansible "Interop19 Ansible Docker").

## Interop19 Network Orchestration Hands-On Showcase
The below instructions are for running an example playbook against the white switch in the Interop19 Network Orchestration Hands-On Showcase.  They can be modified to fit your needs.

## STP Demo interop-stp.yml

After connecting to your docker with `docker exec -it /bin/bash` you should be in `/interop19-ansible/ntc-ansible` automatically.

1. To run the "STP" Playbook with our white switch execute the one below:

` ansible-playbook interop-stp.yml -i interop-hosts`

If Port GigEthernet1 interface is down, the light will turn red, and GigEthernet2 interface will be brought online.

To loop the script, try:

`while sleep 2; do ansible-playbook interop-stp.yml -i interop-hosts; done`

## Light Bulb Challenge
