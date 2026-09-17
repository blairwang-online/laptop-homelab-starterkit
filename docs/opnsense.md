# Opnsense

## Virtualised Opnsense to link up 2 LANs and connect them to WAN

Hypervisor configuration:

- Three VMs running in VirtualBox
    - Ubuntu (workstation)
    - Debian (server)
    - opnsense (virtual appliance)
- 2 x VirtualBox "host-only" networks
    - "Adapter": 192.168.56.1, DHCP on with range 192.168.56.151 to 192.168.56.191
    - "Adapter #2": 192.168.57.1, DHCP on with range 192.168.57.151 to 192.168.57.191

VM networking configuration:

1. Configure opnsense to have
    - Adapter 1 = Host-only adapter (56 series)
    - Adapter 2 = Host-only adapter (57 series)
    - Adapter 3 = NAT (not "NAT Network"!)
2. Boot opnsense, login as root, select option 1 "Assign interfaces"
    - If prompted "Do you want to configure LAGGs now", say "N" for "no".
    - If prompted "Do you want to configure VLANs now", say "N" for "no".
    - When prompted, select `le2` as WAN
    - When prompted, select `le0` as LAN
    - When prompted, select `le1` as "optional interface 1"
    - When prompted, just hit `ENTER` for "optional interface 2"
3. Back at opnsense main menu, using option 2 to "set interface IP address".
    - Assign LAN to have static IP address 192.168.56.101 and OPT1 to have static IP address 192.168.57.101
    - Subnet bit count 24 (no DHCP, no upstream gateway address, no WAN tracking, no DHCP6, no DHCP server, no HTTP web GUI, yes to self-signed web GUI certificate, and yes to restoring web GUI access defaults)
4. Go to `<opnsense ip addr>`/ui/firewall/filter, add new rule to allow traffic to flow between LAN and OPT1
    - Set interface = OPT1
    - Click on Filter and set source = OPT1 network
5. In xubuntu/ubuntu, set static ip addr = 192.168.57.88 gateway 192.168.57.101. Refresh network connection and try to ping 192.168.57.101

IDS configuration:

1. Go to `<opnsense ip addr>`/ui/ids
2. Set enabled = false, try `sudo nmap -sV -O 192.168.56.102`
3. Set enabled = true, capture mode = PCAP live mode (IDS), interfaces = (select all of them). Then download and enable `ET open/emerging-scan`. Confirm rules tab, everything is enabled with mode = ALERT.

IPS configuration:

_(Coming soon...)_
