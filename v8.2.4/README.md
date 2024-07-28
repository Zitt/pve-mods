# pve-mods

Modifications to [Proxmox Virtual Environment](https://www.proxmox.com/en/proxmox-ve) in
order to add CPU and fanspeed values (powered by
[lm-sensors](https://github.com/lm-sensors/lm-sensors)) to the PVE web-based management
interface.

Temperature readings on the desktop version of the management interface:

![PVE GUI desktop screenshot](https://github.com/Zitt/pve-mods/v8.2.4/x299desktop.png?raw=true)

Updates based on the work by Alexleigh at https://github.com/alexleigh/pve-mods.
Mobile updates not provided in this patch.

This patch is specific to [Asus Pro WS X299 SAGE II](https://www.asus.com/motherboards-components/motherboards/workstation/pro-ws-x299-sage-ii/helpdesk_download/?model2Name=Pro-WS-X299-SAGE-II) motherboard running lmsensors v3.6.0. Different motherboards and/or lmsensors may require additional changes or debug. Patches provided AS-IS. 

## Disclaimer

These enhancements involve modifying files distributed by Proxmox packages. As such, they
should be used on hobby projects only. Also, any updates to the affected Proxmox packages
will erase the modifications.

## Requirements

lm-sensors needs to be installed on the hypervisor for the probes to work. To install
lm-sensors, run the following on the hypervisor:

```shell
apt install lm-sensors
```

Hard drive temperatures are skipped here because the Author's system is set to pass thru most of the rust media to a virtual machine.

To access the fan speeds and other temperatures on the motherboard; you will need to [sensors-detect](https://askubuntu.com/questions/53762/how-to-use-lm-sensors) and make the appropriate module changes as outlined when running the application.

```shell
sensors-detect
```
You will need to reboot your pve enviorment after making the sensors-detect changes. 

To confirm the SMART temperature readings are working, run the sensors command on the
hypervisor:

```shell
sensors
```

Verify that fan speeds are detected. 

## Usage

The simple way to apply these modifications is by examining the patch files in one of the patches
directories. Caution: directly applying these patches to the PVE distribution files should only be
done if the PVE packages on your system match the version these patches were generated against. 

Adjust your manual patches as appropriate.
Make backups of your PVE files before patching and I recommend you manually apply the patches with a text editor yourself so that you understand the changes that are being made. 


The patch directories and the versions of the Proxmox packages they were generated against are:


[v8.2.4](v8.2.4/patches)
* pve-manager 8.2.4
* proxmox-widget-toolkit 4.2.1

> **Warning**  
> If the package versions installed on your system are different from these, the patches should not
> be applied. Instead, use the patches as a reference to make manual modifications to the affected
> files.

> **Note**  
> The patches also hardcode the names of various lm-sensors probes to extract temperature readings.
> On your system, the probes you'd like to display and their corresponding names are likely
> different. This is another reason why you might want to make manual modifications rather than
> apply the patch files.

### Making manual modifications

See original [Readme](../README.md) for more information.
