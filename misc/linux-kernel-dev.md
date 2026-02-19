# Linux Kernel Development Guide

This guide covers compiling, configuring, and debugging the Linux kernel for systems research.

---

## Resources

| Resource | Link |
|----------|------|
| Kernel Study Materials | https://kernelmeet.com/topic/2/linux-kernel-study-resources |

---

## Prerequisites

Install required dependencies:

```bash
sudo apt install -y flex bison libncurses5 pkg-config libncurses5-dev libelf-dev libssl-dev
```

---

## Kernel Compilation

### For Physical Machines

```
   git clone https://github.com/torvalds/linux.git
   cd linux
   # check all released kernel versions
   git tag
   # checkout your target kernel version
   git checkout v6.2

   # copy an existing config from the system, choose the one which is closest to the version you try to compile here
   cp /boot/config-XXX .config
   make oldconfig
   # double check if there are some additional features/driver you will to compile
   make menuconfig

   # X -> number of cores on your machine, 40 cores --> it might take ~15min to complete
   make -jX

   # install kernel modules and image
   sudo make INSTALL_MOD_STRIP=1 modules_install
   sudo make install
   sudo update-grub2

   # Now the kernel has been installed, reboot the machine to switch the kernel
   sudo shutdown -r now
```

### For VMs (e.g., FEMU)

For VMs, configure a minimal `.config` to reduce compilation time by excluding unnecessary drivers:

```
   git clone https://github.com/torvalds/linux.git

   cd linux
   # check all released kernel versions
   git tag
   # checkout your target kernel version
   git checkout v6.1

   # configure a mimimal .config
   make defconfig
   make kvm_guest.config # kernel Makefile has recently changed, double check it via "make help"
   # double check if there are some additional features/driver you will to compile, make sure key drivers like "nvme" are included
   make menuconfig

   # X -> number of cores on your machine, 40 cores --> it might take ~15min to complete
   make -jX

   sudo make INSTALL_MOD_STRIP=1 modules_install
   sudo make install
   sudo update-grub2

   # Now the kernel has been installed, reboot the machine to switch the kernel
   sudo shutdown -r now
```

---

## Development Best Practices

| Practice | Why |
|----------|-----|
| **Start with a clean commit** | Enables `git diff` to compare against original source |
| **Use `printk()` liberally** | Simple but effective debugging approach |
| **Add enable/disable switches** | Test with changes disabled first |
| **Make small, incremental changes** | Easier to find bugs |
| **Enable debugging symbols** | Shows function+offset when bugs occur |

### Git Commit Strategy

Before making changes, commit the clean kernel state:

```
* EOI handling
|
* Add Injection mode
|
* Shadow IDT Initialization
|
* Original Kernel Source code   <-- Start here
```

### Debugging with printk()

Add `printk()` calls throughout your code changes:

```c
printk("shadow-idt: Initializing Shadow IDT");
ShadowIDT();
printk("shadow-idt: Shadow IDT Initialization Success");
```

### Feature Flags

Always add a switch to enable/disable your changes. This lets you:
1. Test with changes disabled first
2. Enable features incrementally
3. Isolate issues quickly

---

## Future Documentation (TODO)

- Kernel function tracing (ftrace)
- Debugging kernel via `gdb` + `qemu`

---

## Kernel Configuration (menuconfig)

To customize kernel options:

```bash
make menuconfig
```

### NVMe Configuration

Navigate to `Device Drivers → NVME Support` and enable all options:

![NVMe](https://drive.google.com/uc?export=view&id=1PK3Yiu2pCJILAmFnOHIqg73Q9f4kjBQG)

### ZNS Configuration

ZNS requires several additional features:

| Feature | Menu Path | What to Enable |
|---------|-----------|----------------|
| **Block Layer** | `Enable the block layer` | Zoned block device support |
| **IO Scheduler** | `Enable the block layer → IO Scheduler` | mq-deadline I/O scheduler |
| **Device Mapper** | `Device Drivers → Multiple devices driver support` | Drive-managed zoned block device target |
| **File System** | `File systems` | zonefs filesystem support |

#### Block Layer
![Block Layer](https://drive.google.com/uc?export=view&id=13RVNxleilWZ7BZSzBda04P8elaen4MQS)

#### IO Scheduler (mq-deadline)
![mq-deadline](https://drive.google.com/uc?export=view&id=1lBApoa-Ljw9AW2Xx00rdA1pZw-i4Syrm)

#### Device Mapper
![device mapper](https://drive.google.com/uc?export=view&id=1TCDsW6-andR6DmCi-j_WY7BjU9RFwZnT)

#### File System (zonefs)
![File System](https://drive.google.com/uc?export=view&id=1vOdH8qKfojG3Y4Nq-shWgK3pj9mwN_8p)
