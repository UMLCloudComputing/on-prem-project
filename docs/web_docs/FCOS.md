## Fedora CoreOS (FCOS) Notes

### About

Container Operating System meaning it is built for running container workloads.

Supported for OKD 4

Based on Fedora so FCOS software is in RPM packages and each one uses the Fedora kernel.

Immutable so core components are read-only and cannot be modified ensuring stability. Immutability here is useful so you can store the latest state in the cluster so it can be used to create addition machines and perform updates based on the latest FCOS configurations.

For container runtime it provides CRI-O instead of the Docker engine. It does has features for running OCI & libcontainer formatted containers that Docker requires. CRI-O offers a smaller footprint and reduced attack surface due to smaller feature set.

FCOS replaces Docker CLI tools with a compatible set of container rools. 
Podman CLI for running, starting, stopping, listing, removing, etc.
Skopeo CLI for copying, authenticating, and signing images.
crictl for interacting with CRI-O

Transactional upgrades using rpm-ostree. Updates are delivered through container images. When deployed the container image is pulled, extracted, and written to disk then the bootloader is modified to boot into the new version.

Machine Config Operator for OKD handles the updates for that.

FCOS systems and the layout of RPM-Ostree file systems have the following characteristics:
/usr is where the operating system binaries and libraries are stored and it is read-only
/etc, /boot, /var are writable on the system
/var/lib/containers is the graph storage location for storing container images

### Configuration

Day 1 customizations for changes that need to be made when the cluster is first up. These are done through ignition files.

Things you can customize:
- Kernel Args
- Disk Encryption
- Kernel Modules
- Chronyd (Specific clock settings)

### Deployment

For OKD related FCOS installations you do it based on deploying on infrastructure provisioned by the installer or by the user. 

Installer-provisioned: Cloud environments might have preconfigured infrastructures that can be used for OKD clusters. You can supply the ignition with content to place on each node.

User-provisioned: You can add what content you want. Also best to do through ignition.

### Ignition

Utility used during initial configuration. Completes common disk tasks like partitioning, formatting, writing files, and configuring users. 

On first boot this the ignition is read and does the configuration from the install media or the location that you specify and then applies the configuration to the machines.

Similar to tools like cloud-init or Linux Anaconda kickstart. 

Runs from an initial RAM disk separate from the system you are installing to. This allows for the partition operations to occur. 

Meant to init systems not change existing systems.

After the Ignition finishes configuring a machine, the kernel keeps running but discards the initial RAM disk and pivots to the installed system on disk.

Ignition confirms that all new machines meet the declared configuration so you cannot have a partially configured machine. If something fails Ignition does not start the new machine. So in OKD's case the cluster will never be partially configured and if it's being added to the cluster then it will never be added.

Order of information in an Ignition does not matter it will figure out what needs to go first and such.

Because it can start on an empty hard disk it can be used to set up bare metal. cloud-init cannot do that.

#### Ignition Sequence for an FCOS machine in an OKD cluster
1) Machine gets its Ignition config file. Control plane machines get their Ignition config files from the bootstrap machine and worker machines get theirs from control plane machines.

2) Ignition creates disk partitions, file systems, directories, and links on machine. RAID arrays are support but does not support LVM volumes.

3) Ignition mounts the root of the permanent file system to the /sysroot directory in the initramfs and starts working in that directory.

4) Ignition configures all defined file systems and sets them up to mount appropriately at runtime.

5) Ignition runs systemd temp files to populate required files in the /var directory

6) Ignition runs the ignition config files to set up users, systemd unit files, and other config files

7) Ignition unmounts all components in the permanent system that were mounted in the initramfs

8) Ignition starts up the init process of the new machine, which in turn starts up all other services on the machine that run during system boot.


Notes from: https://docs.okd.io/latest/architecture/architecture-rhcos.html
