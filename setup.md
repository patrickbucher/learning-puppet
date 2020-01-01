# Virtual Box under Arch Linux

Install virtualbox and modules needed:

    pacman -S virtualbox virtualbox-guest-modules-arch virtualbox-host-dkms linux-headers

TCP port forward from port 8022 (host) to port 22 (guest) for SSH:

    ssh -p 22 root@localhost

# Debian using qemu under Arch Linux

## Get the Image

- Download [netinst](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-10.2.0-amd64-netinst.iso) image
- Verify SHA512 sums against [SHA512SUMS](http://cdimage.debian.org/debian-cd/current/amd64/iso-cd/SHA512SUMS)

## Install Packages

Install qemu:

    pacman -S qemu

Make sure user is in libvirt and kvm group:

    usermod -a -G libvirt paedu


## Setup

Create Disk Image (8 Gigs):

    qemu-img create -f qcow2 debian.qcow2 8G

Run setup from netinst image:

    qemu-system-x84_64 -enable-kvm \
        -m 2048 -boot d -net nic -net user \
        -hda debian.qcow2 -cdrom debian-10.2.0-amd64-netinst.iso

Run the image with SSH port fowarding (host 8022 to guest 22):

    qemu-system-x84_64 -enable-kvm \
        -m 2048 -boot d -net nic -net user,hostfwd=tcp::8022-:22 \
        -hda debian.qcow2

SSH connect to VM:

    ssh -p 8022 user@localhost
