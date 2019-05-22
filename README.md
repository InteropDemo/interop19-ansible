## Setup Ansible Docker




## Modify interop.yml files

[link text](http:// interop "alt").

After connecting to your docker with `docker exec -it /bin/bash` you should be in `/interop19-ansible/ntc-ansible`

1. To run the "STP" Playbook with our white switch execute the one below:

` ansible-playbook interop-stp.yml -i interop-hosts`

If Port GigEthernet1 interface is down, the light will turn red, and GigEthernet2 interface will be brought online.

To loop the script, try:

`while sleep 2; do ansible-playbook interop-stp.yml -i interop-hosts; done`
