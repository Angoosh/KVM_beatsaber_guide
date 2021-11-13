# KVM_beatsaber_guide
Guide how to setup beatsaber inside kvm on Oculus Rift S<br>
Distribution used is Arch, but it should be the same on any distro

## Hardware used
CPU: intel i7 7700K<br>
RAM: 32G<br>
GPU: nvidia quadro K2200<br>
USB card: AXAGON PCEU-430VL<br>

## Prerequisities
Windows 10 virtual machine with GPU passthrough through qemu, there are great guides on the internet eg.:https://wiki.archlinux.org/title/PCI_passthrough_via_OVMF<br>
VM should have at least 8GB of ram allocated, preferably 16GB<br>
VR headset<br>
Steam account<br>
Laptop or another PC on the same network with virt-viewer installed.<br>

## Lets get to it
Pass pcie usb card to VM (same as gpu passthrough)<br>
Allocate at least 6 threads to your VM. In virt-manager cpu configuration should be host-passthrough and manual topoloy with for my example 3 cores and 2 threads for each core.<br>
Make sure you don't have external display connected to your gpu only the headset.<br>
I use spice as display server and connect to it with my laptop because of the CPU resources which cause bad lag through songs.<br>
For spice server configuration it should look something like this:
```
<graphics type="spice" autoport="yes" listen="0.0.0.0">
  <listen type="address" address="0.0.0.0"/>
  <image compression="auto_glz"/>
  <streaming mode="filter"/>
</graphics>

```
Also make sure your firewall is configured to pass packets to and from port 5900 or other spice port you select<br>
Other things to edit in VM:
```
<domain type="kvm" xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'>
```
After you install steam and download Oculus software and Beatsaber, setup your headset as you would normally do and when you're done remove network controller from VM. This helps mostly with annoying beatsaber updates and from windows updates, whch really hurt performance.<br>
Set windows power management to `performance` and your CPU governor to performance aswell, but this shouldn't be nessesary.<br>
Only thing to do now is to enjoy Beatsaber. If you want to add more maps into it, just use usb flash drive which will be passed through spice into your VM.<br>
This works for me even on the ancient quadro from 2014 and the performance is quite good and it should be a cheap card even now with chip shortage.
