## Origin Kubernetes Distribution (OKD) Notes

### What is it?
- OKD is the upstream for OpenShift
- Includes: web console, auth, image registry, monitoring, networking, operator management

### Installation Information

There are four types of ways to install OKD
- Interactive: Web based installer. Needs internet. Provides smart defaults and preforms pre-flight validations before installing the cluster. Also has a RESTful API for automation & advanced config.
- Local Agent-Based: Local for disconnected environments. Has same benefits of the web based assisted just requires you to download it and configure it first. Done through a CLI.
- Automated: Uses a Baseboard Management Controller* for provisioning. 
- Full Control: You deploy the cluster on infrastructure that you prepare and maintain for full maximum customizability. 

Installation program generates the main assets such as ignition config files for bootstrap, control plane, and compute machines.

For more info on Fedora CoreOS & Ignitions see the FCOS.md.

Installation program has a set of targets & dependencies that it must achieve. 

Each cluster machine uses Fedora CoreOS as the OS.

Baseboard Management Controller - small processor on a motherboard that allows for remote management and monitoring of the system's hardware, independent of the main OS.

### Useful Docs Links:
- https://docs.okd.io/latest/architecture/architecture.html
- https://docs.okd.io/latest/installing/overview/index.html
