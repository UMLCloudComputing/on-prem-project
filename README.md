# on-prem-project

# Networking
## Opnsense and Teleport
### LAN
IPv4
- DHCP Range: `10.0.0.0 - 10.0.1.255`
- Static IP Range: `10.0.2.0 - 10.0.7.255`

Total Range: `10.0.0.1/21`, `10.0.0.0 - 10.0.7.255`

### Reserved Static IPs
- okd-services: `10.0.3.5`
- teleport: `10.0.2.0`

### Networking Diagram
![Networking Diagram](./images/network-diagram)

