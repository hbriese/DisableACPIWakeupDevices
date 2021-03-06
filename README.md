
# acpi_wakeup
> Disable/enable ACPI wakeup devices

[![License](http://img.shields.io/badge/license-APACHE2-blue.svg)]()

#### Install
```bash
$ git clone https://github.com/hbriese/acpi_wakeup.git
$ sudo acpi_wakeup/install.sh
```


## Usage
#### List ACPI wakeup devies
```bash
$ acpi_wakeup -l
```


#### Keep enabled specified wakeup devices (persistent)
Device names (or sysfs nodes) that you want ACPI wakeups enabled for. Supports regular expressions.

Edit /etc/acpi_wakeup.conf with each device on a new line.

_e.g. Keep awake PBTN (power button), LID devices (e.g. LID...), and a particular PCI devices._
```text
> /etc/acpi_wakeup.conf
# Comments after a hash
PBTN
LID[\d]*
pci:0000:00:14.0
```

> _Default devices enabled:  PBTN LID[\d]*_

**It is recommended to specify devices by their sysfs node (e.g. pci:...) if the device name is not unique.**


#### Keep enabled specified wakeup devices (non-persistent)
_Overrides devices in /etc/wakeup-devices.conf_
```bash
$ acpi_wakeup -s -d DEVICE DEVICE ...
```

_e.g._
```bash
$ acpi_wakeup -s -d PBTN LID[\d]* pci:0000:00:14.0
```


##### Disable ALL devices (non-persistent)
Use --devices (-d) without any options to disable all wakeup devices.
```bash
$ acpi_wakeup -s -d
```


#### Set wakeup devices
Automatically executed on start by systemd.

Use with other options for them to have an affect.

```bash
$ acpi_wakeup -s
```
