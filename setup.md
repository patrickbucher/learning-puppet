# Arch Linux

Install virtualbox and modules needed:

    pacman -S virtualbox virtualbox-guest-modules-arch virtualbox-host-dkms linux-headers

TCP port forward from port 8022 (host) to port 22 (guest) for SSH:

    ssh -p 22 root@localhost
