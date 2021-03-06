## What is netboot.xyz?

[netboot.xyz](http://www.netboot.xyz) is a convenient place to boot into any type of operating system or utility disk without the need of having to go spend time retrieving the ISO just to run it.  iPXE is used to provide a user friendly menu from within the BIOS that lets you easily choose the OS you want along with any specific types of versions or bootable flags.

You can remote attach the ISO to servers, set it up as a rescue option in Grub, or even set your home network to boot to it by default so that it's always available.

### Getting started

Grab these bootloaders and drop them into your favorite virtualization tool to start testing out netboot.xyz.  These are precompiled versions of the latest version of [iPXE](http://https://github.com/ipxe/ipxe) that will chainload you to [http://boot.netboot.xyz/menu.ipxe](http://boot.netboot.xyz/menu.ipxe).  There are two versions of each, one if you have DHCP on your network, and one if you have to set a static IP before connecting outside of your network.

* ISO: [dhcp](http://boot.netboot.xyz/ipxe/netboot.xyz-dhcp.iso) | [static](http://boot.netboot.xyz/ipxe/netboot.xyz-static.iso)
* Floppy/USB: [dhcp](http://boot.netboot.xyz/ipxe/netboot.xyz-dhcp.dsk) | [static](http://boot.netboot.xyz/ipxe/netboot.xyz-dhcp.dsk)
* Linux Kernel: [dhcp](http://boot.netboot.xyz/ipxe/netboot.xyz-dhcp.lkrn) | [static](http://boot.netboot.xyz/ipxe/netboot.xyz-static.lkrn)
* [SHA256 Checksums](http://boot.netboot.xyz/ipxe/netboot.xyz-sha256-checksums.txt)

If you already have iPXE up and running on the network, you can hit netboot.xyz at anytime by typing:

    chain --autofree http://boot.netboot.xyz

### Booting Methods
#### NIC with Embedded iPXE

If you've already compiled your own iPXE, you can load up the netboot.xyz menu easily by entering CTRL-B when prompted setting DHCP and then chainloading iPXE:

    dhcp
    chain http://boot.netboot.xyz/menu.ipxe

If you don't have DHCP on your network, you can manually set your network information:

    set net0/ip <ip>
    set net0/netmask <netmask>
    set net0/gateway <gateway>
    set dns <nameserver>
    ifopen net0
    chain http://boot.netboot.xyz/menu.ipxe

#### Boot from iPXE ISO

To create a bootable CD-ROM, burn the ISO image ipxe.iso (~1MB in size) to a blank CD-ROM.  You can also use this ISO file as a virtual CD device in Citrix XenServer, VMware ESXi, VMware Fusion, VirtualBox, or even in a Dell DRAC or HP iLOs virtual CD drive.

#### Boot from iPXE USB

*Warning: Backup your important data before using USB as it will overwrite anything on the USB key.*

Insert a USB disk, find it's device name of USB. Then use following command:

    cat ipxe.dsk > /dev/sdX

or

    dd if=ipxe.dsk of=/dev/sdX

where sdX is your usb drive.  Substitute /dev/sdX for /dev/fd0 in the case of using a floppy.

### Operating Systems

#### What Operating Systems are currently available on netboot.xyz?

* [ArchLinux](https://www.archlinux.org)
* [CentOS](https://centos.org)
* [CoreOS](https://coreos.com/)
* [Debian](https://debian.org)
* [Fedora](https://fedoraproject.org)
* [FreeBSD](https://freebsd.org)
* [Gentoo](https://gentoo.org)
* [Kali](https://www.kali.org)
* [OpenBSD](http://openbsd.org)
* [OpenSUSE](http://opensuse.org)
* [RancherOS](http://rancher.com/rancher-os/)
* [Scientific](http://scientificlinux.org)
* [TinyCoreLinux](http://distro.ibiblio.org/tinycorelinux/)
* [Ubuntu](http://www.ubuntu.com/)
* [WinPE](http://www.microsoft.com/)

#### Utilities

* [Clonezilla](http://www.clonezilla.org/)
* [GParted](http://gparted.org)
* [HDT](http://www.hdt-project.org/)
* [Memtest](http://www.memtest.org/)
* [Partition Wizard](http://www.partitionwizard.com)

### Contributing

Pull requests are welcome and encouraged.  Feel free to issue a pull request for new versions or tools that you might find useful.  Once merged into master, travis-ci will regenerate new versions of iPXE from upstream and deploy the latest changes to netboot.xyz.

### Testing New Branches

Under the Utilities menu on netboot.xyz, there's an option for "Test netboot.xyz branch".  If you've forked the code and have developed a new feature branch, you can use this option to chainload into that branch to test and validate the code.  All you need to do is specify your github user name and the name of your branch or abbreviated hash of the commit.

### Feedback

Feel free to open up an issue on github or contact me via <antony@mes.ser.li>.
