# Cisco PNP without APIC/DNAC

Credits to : 
- https://github.com/dmfigol/cisco-pnp-server
- https://github.com/pmeffre/ciscopnp

## Execution
change the variable HTTP Server in ./configs/vars.py to your Servers IP:Port

```shell
pip install -r requirements.txt
python3 main.py
```
### Options

define different return IP for the PnP Requests (NAT)
```sh
./main.py -i 1.1.1.1
# or
./main.py --ip 1.1.1.1
```
default the Server will run on Port:8080 this can be changed
```sh
./main.py -p 8081
# or
./main.py --port 8081
```

## How to use

You have to create a config directory (./configs) which must contain:

 - "Serial Number of Switch".cfg

Configure your DHCP to point a blank Device to the PnP Server via DHCP Option 43 value: 5A1D;K4;B2;I198.18.168.3;J8080

- 5: DHCP sub-option for PnP
- A: feature-code for Active
- 1: Version
- D: Debug On

- K: Defines the Transport Protocol as 4 = HTTP
- B: Defines the Server Adress as 2 = IPv4
- I: is your Servers IP
- J: Server Port

Reference: [Cisco Devnet Open-PnP](https://developer.cisco.com/site/open-plug-n-play/learn/learn-open-pnp-protocol/)

The Device will discover the PnP Server on boot via DHCP and query the PnP, which will respond to the Device to fetch a file based on the Device Serial Number serial.cfg.

Can be used in combination with: [oliverl-21/ansible-role-ios_config](https://github.com/oliverl-21/ansible-role-ios_config) via PnP Flow with a dynamic CSV Inventory

## To-Do

Describe the Dynamic Inventory part and usage with Ansible.

## Tested

- cat8kv
  - &#9745; IOS-XE 17.5.1
  - &#9745; IOS-XE 17.4.2
- cat 9200(l)
  - versions
- cat 9300
  - versions

&#9745; Tested and working
&#9744; not tested
&#9746; not working
