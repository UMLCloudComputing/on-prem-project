# on-prem-project

This repository contains documentation and files related to the UML Cloud Computing Club's on prem infrastructure.

## Hardware

TODO: Fill in information about our hardware

## Software

Hypervisor: Proxmox

Internal Router: Opnsense

DNS Server: Bind

## Networking

### Opnsense and Teleport

#### LAN

IPv4

- Static IP Range: `10.0.0.0 - 10.0.1.255`
- DHCP Range: `10.0.2.0 - 10.0.7.255`

Total Range: `10.0.0.1/21`, `10.0.0.0 - 10.0.7.255`

### Reserved/Static IPs (vm-name: LAN, WAN)
- dns: `10.0.0.2`
- teleport: `10.0.0.3`, `192.168.6.100`
- opnsense(gateway): `10.0.0.1`, `192.168.6.101`
- okd-services: `10.0.0.30`
- okd-bootstrap: `10.0.0.31`
- okd-control1: `10.0.0.32`
- okd-control2: `10.0.0.33`
- okd-control3: `10.0.0.34`
- okd-worker1: `10.0.0.35`
- okd-worker2: `10.0.0.36`

#### Local DNS Records

`pihole.umlcloudcomputing.local` -> `10.0.0.2`
`teleport.umlcloudcomputing.local` -> `10.0.0.3`

#### Networking Diagram

![Networking Diagram](./images/network-diagram.png)
