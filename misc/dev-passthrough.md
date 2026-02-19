# PCIe Device Passthrough Guide

This guide explains how to pass PCIe devices (NVMe SSDs, network cards, etc.) through to QEMU VMs using VFIO.

---

## Prerequisites

Ensure IOMMU is enabled in your kernel:

```bash
# Add to /etc/default/grub in GRUB_CMDLINE_LINUX_DEFAULT
intel_iommu=on iommu=pt

# Update grub and reboot
sudo update-grub
sudo reboot
```

---

## Step-by-Step Passthrough

| Step | Action | Command |
|:----:|--------|---------|
| 1 | Find device PCIe ID | `lspci` (e.g., `0000:02:00.0`) |
| 2 | Unbind from host | `./vfio-bind 0000:02:00.0` |
| 3 | Add to QEMU | `-device vfio-pci,host=02:00.0` |
| 4 | Start VM | Device appears via `lspci` in guest |

### To Return Device to Host

Use `vfio-unbind` to re-bind the device to the host OS for direct testing.


---

## Helper Scripts

### vfio-bind

Binds a PCIe device to the VFIO driver for VM passthrough:

```bash
#!/bin/bash

#modprobe vfio enable_unsafe_noiommu_mode=1
modprobe vfio-pci
modprobe vfio_iommu_type1

for dev in "$@"; do
        vendor=$(cat /sys/bus/pci/devices/$dev/vendor)
        device=$(cat /sys/bus/pci/devices/$dev/device)
        if [ -e /sys/bus/pci/devices/$dev/driver ]; then
                echo $dev > /sys/bus/pci/devices/$dev/driver/unbind
        fi
        echo $vendor $device > /sys/bus/pci/drivers/vfio-pci/new_id
done
```

**Usage:** `./vfio-bind 0000:02:00.0`

### vfio-unbind

Returns a device to the host OS:

```bash
#!/bin/bash

#modprobe vfio-pci

for dev in "$@"; do
        vendor=$(cat /sys/bus/pci/devices/${dev}/vendor)
        device=$(cat /sys/bus/pci/devices/${dev}/device)
        if [ -e /sys/bus/pci/devices/${dev}/driver ]; then
                echo "${dev}" > /sys/bus/pci/devices/${dev}/driver/unbind
        fi
done
```

**Usage:** `./vfio-unbind 0000:02:00.0`

---

## Notes

- Ensure VFIO drivers are loaded in the host kernel (especially for custom-compiled kernels)
- The device will no longer be visible to the host after binding to VFIO
