# Vagrant Multi-Machine Configuration

This repository contains an example configuration for a multi-machine environment using Vagrant and VMware ESXi.

## Prerequisites

- Installed [Vagrant](https://www.vagrantup.com/)
- VMware ESXi installed with appropriate credentials
- An existing network with DHCP or manual IP setup
- The Vagrant-VMware-ESXi plugin extension

## Configuration Details

The Vagrant file defines a Kubernetes-like cluster environment with the following machines:

| Name        | Operating System | vCPUs | RAM (MB) | Storage (GB) |
|------------|----------------|--------|---------|--------------|
| k8s-master | CentOS 7       | 2      | 4096    | 21           |
| k8s-node1  | CentOS 7       | 2      | 2048    | 22           |
| k8s-node2  | CentOS 7       | 2      | 2048    | 22           |
| k8s-node3  | CentOS 7       | 2      | 2048    | 22           |

### VMware ESXi Configuration

- **Host:** `192.168.2.10`
- **User:** `root`
- **Network:** `VM Network`
- **CPU, RAM, Storage:** As specified above
- **Network Adapter:** `vmxnet3`
- **Synced Folder:** `/Vagrantfiles` using `rsync`

## Usage

1. **Start the Vagrant environment**

   ```sh
   vagrant up --provider=vmware_esxi
   ```

2. **Start an individual machine**

   ```sh
   vagrant up k8s-master --provider=vmware_esxi
   ```

3. **Connect to a machine**

   ```sh
   vagrant ssh k8s-master
   ```

4. **Shut down all machines**

   ```sh
   vagrant halt
   ```

5. **Destroy all machines**

   ```sh
   vagrant destroy
   ```

## Customization

- Resource configurations (vCPUs, RAM, Storage) can be adjusted in the `Vagrantfile`.
- VMware ESXi network and datastore settings can be customized in the respective sections.
- Additional machines can be added by modifying the `nodes` hash in the `Vagrantfile`.

## License

MIT License
