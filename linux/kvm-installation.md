# KVM/Installation

![Image by 3nions](https://www.3nions.com/wp-content/uploads/2018/10/What-is-a-Linux-KVM-VPS-and-Why-Are-They-Reliable.png)

[KVM](https://www.linux-kvm.org/page/Main_Page) (Kernel-based Virtual Machine) is an open-source virtualization technology built into the Linux kernel. It allows you to run multiple isolated guest virtual machines based on Linux or Windows. Each guest has its own operating system and dedicated virtual hardware such as CPU(s), memory, network interfaces and storage.

## Table Of Contents

1. [Intro](#intro)

2. [Prerequisites](#prerequisites)

3. [Installation](#installation)

4. [Network Setup](#network-setup)

5. [Reference](#reference)

## Intro

The problem came when I installed the [Android Studio IDE](https://developer.android.com) for mobile device development, where in the installation process a message appeared that your system didn't have an emulator and I was directed to install KVM first.

Therefore I will make notes again to help me someday in the process of installing and configuring KVM on Ubuntu Desktop 18.04.1

## Prerequisites

To be able to run guests with more than 2 GB of RAM, and to host both 32-bit and 64-bit KVM guests, you must have a 64-bit host system.

Before continuing with the installation, make sure your Ubuntu host machine supports KVM virtualization. Enter the following [`grep`](https://linuxize.com/post/how-to-use-grep-command-to-search-files-in-linux/) command to see if your processor supports hardware virtualization:

```bash
$ grep -Eoc '(vmx|svm)' /proc/cpuinfo
```

> If your CPU supports hardware virtualization, the command will output a number greater than zero, which is the number of the CPU cores. Otherwise, if the output is `0` it means that the CPU doesn’t support hardware virtualization.

By default, if you booted into XEN kernel it will not display svm or vmx flag using the grep command. To see if it is enabled or not from xen, enter:

```bash
$ cat /sys/hypervisor/properties/capabilities
```

You must see hvm flags in the output. Alternatively, you may execute:

```bash
$ kvm-ok
```

which may provide an output like this:

```bash
INFO: /dev/kvm exists
KVM acceleration can be used
```

but if you see this, you can still run virtual machines, but it'll be much slower without the KVM extensions.

```bash
INFO: Your CPU does not support KVM extensions
KVM acceleration can NOT be used
```

## Installation

Run the following command to install KVM and additional virtualization management packages:

```bash
$ sudo apt install qemu-kvm libvirt-bin bridge-utils virtinst virt-manager
```

- `qemu-kvm` - software that provides hardware emulation for the KVM hypervisor.
- `libvirt-bin` - software for managing virtualization platforms.
- `bridge-utils` - a set of command-line tools for configuring ethernet bridges.
- `virtinst` - a set of command-line tools for creating virtual machines.
- `virt-manager` provides an easy-to-use GUI interface and supporting command-line utilities for managing virtual machines through libvirt.

Once the packages are installed, the libvirt daemon will start automatically. You can verify it by running:

```bash
$ sudo systemctl is-active libvirtd
```

To be able to create and manage virtual machines, you’ll need to add your user to the “libvirt” and “kvm” groups. To do that, type in:

```bash
$ sudo usermod -aG libvirt $USER
$ sudo usermod -aG kvm $USER
```

> `$USER` is an environment variable that holds the name of the currently logged-in user. Log out and log back in so that the group membership is refreshed.

## Network Setup

A bridge device called “virbr0” is created by default during the libvirt installation process. Run the `brctl` tool to list the current bridges and the interfaces they are connected to:

```bash
$ brctl show
```

```bash
# Output
bridge name    bridge id            STP enabled    interfaces
virbr0         8000.5254002c83cf    yes            virbr0-nic
```

> The “virbr0” bridge does not have any physical interfaces added. “virbr0-nic” is a virtual device with no traffic routed through it. The sole purpose of this device is to avoid changing the MAC address of the “virbr0” bridge.

This network setup is suitable for most Ubuntu desktop users but has limitations. If you want to access the guests from outside the local network, you’ll need to [create a new bridge](https://help.ubuntu.com/community/KVM/Networking#Bridged_Networking) and configure it so that the guest machines can connect to the outside world through the host physical interface.

## Reference

- Configure VM acceleration on Linux - [Android Studio Docs](https://developer.android.com/studio/run/emulator-acceleration?utm_source=android-studio#vm-linux)
- Ubuntu KVM Installation - [Help Ubuntu](https://help.ubuntu.com/community/KVM/Installation)
