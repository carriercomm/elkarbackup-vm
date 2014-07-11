# elkarbackup-vm

We are using [VirtualBox](http://www.virtualbox.org), [Packer](http://www.packer.io) & [Ansible](http://www.ansible.com/home) to generate an **updated Elkarbackup virtual machine** for demo/appliance purposes:

**Packer** creates consistent images for multiple platforms in parallel. It's perfect for creating appliances and disposable product demos.

Required:
 * VirtualBox 4.1.12 or higher

## Instructions

```bash
# Download dependencies
./bootstrap.sh
# Build VM image
./build.sh
```

An updated ElkarBackup virtual machine, compatible with **VirtualBox** or **VMWare** (not tested), will be created on `output-vm/elkarbackup-vm.ova`

### Other formats

Once we have OVA file, we can convert it to other formats:

**KVM/QCOW2** (Proxmox compatible)
```bash
tar -xvf elkarbackup-vm.ova
qemu-img convert -O qcow2 elkarbackup-vm-disk1.vmdk elkarbackup-vm.qcow2
```

## Develop & Testing

We also use this code for developing or testing purposes, thanks to [Vagrant](http://www.vagrantup.com)

Required:
 * Vagrant 1.6.2 or higher
 * Ansible 1.6 or higher

We will use an empty Debian Wheezy Vagrant box and some Ansible roles to generate our development environment:

```bash
$ cd dev
$ vagrant up
$ vagrant ssh
```

You can modify ElkarBackup source on `/opt/elkarbackup` and you will see your changes inmediatelly in your browser at http://192.168.33.10/elkarbackup


### Troubleshooting

**SSH encountered an unknown error during the connection**.

You can try again with `vagrant provision` or you can try this:

Create file `.ssh/config`:

```
Host 127.0.0.1
        StrictHostKeyChecking no
        UserKnownHostsFile=/dev/null
```

[More info](http://www.midwesternmac.com/blogs/jeff-geerling/fixing-ssh-unknown-error-when)
