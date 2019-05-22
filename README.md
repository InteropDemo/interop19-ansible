# Interop19 Network Orchestration Hands-On Showcase
The below instructions are for running an example playbook against the white switch in the Interop19 Network Orchestration Hands-On Showcase.  They can be modified to fit your needs.

## Setup Ansible Docker

1. Setup the Ansible Container in Docker: [Interop19-Docker/Ansible](https://github.com/InteropDemo/interop19-docker/tree/origin/master/ansible "Interop19 Ansible Docker").

## Auto Remediation Demo

The `interop-stp.yml` Ansible playbook's primary purpose is to detect and provide auto-remediation of a down or redundant uplink port on the white demo lab switch (included in the `interop-hosts` inventory file).  

After running this playbook, if both uplink ports are connected (GigEthernet1 and GigEthernet2), the playbook will make an API call to change the lightbulb to Green, and shutdown the redundant uplink port (GigEthernet2).  

However, if GigEthernet2 is shutdown, and the link on GigEthernet1 is physically lost (unplugged), the playbook will make an API call to change the lightbulb to Red, and repair the uplink by enabling the GigEthernet2 connection.

### To get started:

2. After connecting to your docker with `docker exec -it /bin/bash` you should be in `/interop19-ansible/ntc-ansible` automatically.

3. Download the latest changes to the repository by running:
```console
git pull
```

4. To run the "STP" Playbook with our white switch execute the one below:
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
