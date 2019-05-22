## Setup Ansible Docker

1. Setup the Ansible Container in Docker: [Interop19-Docker/Ansible](https://github.com/InteropDemo/interop19-docker/tree/origin/master/ansible "Interop19 Ansible Docker").

## Interop19 Network Orchestration Hands-On Showcase
The below instructions are for running an example playbook against the white switch in the Interop19 Network Orchestration Hands-On Showcase.  They can be modified to fit your needs.

## STP Demo interop-stp.yml

After connecting to your docker with `docker exec -it /bin/bash` you should be in `/interop19-ansible/ntc-ansible` automatically.

2. Download the latest changes to the repository by running:
```console
git pull
```

3. To run the "STP" Playbook with our white switch execute the one below:
```console
ansible-playbook interop-stp.yml -i interop-hosts
```

If Port GigEthernet1 interface is down, the light will turn red, and GigEthernet2 interface will be brought online.

To loop the script, try:
```console
while sleep 2; do ansible-playbook interop-stp.yml -i interop-hosts; done
```

## Light Bulb Challenge

For the lightbulb challenge, the following challenges are available.  The goal is to detect one of the following conditions, and include the appropriate lightbulb API playbook if the condition is true:

- VLAN ID Present
  - bluelight.yml
- Static MAC Address Found (Directly Connected)
  - purplelight.yml
- Route Exists
  - yellowlight.yml
- CDP Neighbor Found
  - whitelight.yml
  
Refer to the interop-stp.yml file for conditonal includes. Hint:
```
- include: bluelight.yml
  when: "'phrase' in varableName"
  vars:
    variableName: "{{ hostvars['deviceName']['response']['itemName']
```
