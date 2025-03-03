# Proxmox Tuya-Convert v2.0 Container 

### Updated Sept 27 (1:00am EST) Now Tuya 1.0 Compatible & Light Bulb compatible (so far...) 

#### Testing note: Many devices have been successfully flashed. Reports of success with Light-Bulbs have started to appear, and this branch has been updated accordingly. NOTE: You will wait longer (more dots) for some of these devices - this is NORMAL - be patient.  This message will be removed once Tuya 2.0 is considered completed... Check daily as there is a lot of work happening on this topic ATM.

This script will create a Proxmox LXC container with the latest Debian-BUSTER and setup tuya-convert. This process is still experimental and very somewhat tempermental. 

To create a new LXC container in the `local-lvm` storage, run the following in a SSH session or the console from Proxmox interface

```
bash -c "$(wget -qO - https://raw.githubusercontent.com/sirredz/proxmox_tuya-convert_container/master/create_container.sh)" -s local-lvm
```

During the setup process, you will prompted to select a wireless interface. This interface will be assigned to container. _(Note: When the container is running, no other container or VM will have access to the interface.)_ After the successful completion of the script, start the container identified by the script, then use the login credentials shown to start the tuya-convert script. If you need to stop tuya-convert, press `CTRL + C` and it will be halted and you will be brought back to the login prompt. If you login again it will start tuya-convert again.

Note: A new GUI prompt will appear about updating SMB.CONF - just select NO <Default> and press ENTER to continue the script. It will wait for a response.

## Prerequisites

In order for this script to work appropriately, you must first have the wireless NIC's drivers installed and setup correctly for your WiFi adapter in Proxmox. The beginning the of the script will test for valid WLAN interfaces. An error will be produced if one can not be found.

## Custom Firmware

To add custom firmware (not supplied by tuya-convert), connect to the samba share created by the container (details are provided at the login prompt) and add the binary to the `tuya-convert/files/` folder. Your binary will listed under the custom firmware menu.

DigiblurDIY has provided the latest Tasmota BIN files with WiFiManager enabled (thirdpary.bin) - Thanks Travis!
All you have to do is start your Tuya-Convert container, and drop the BIN file in the files folder using SAMBA bfore you start the conversion process. The script will index the folder contents for you.

## It is highly recommended you flash thirdparty.bin with the WIFI Manager enabled by default. This will prevent 'bricking' the device as a result of typing the SSID or PASSWORD incorrectly, during setup.

## Sources

DigiBlur's WIFIMANAGER (default) compiled Sonoff-Tasmota builds

https://github.com/digiblur/Sonoff-Tasmota/tree/development/generic

Tuya-Convert 1.0 Github (for Raspberry Pi 3/3B) or (Kali-Linux/Debian with proper dependancies already setup)

https://github.com/ct-Open-Source/tuya-convert

Tuya-Convert 2.0 Github (for Raspberry Pi 3/3B) or (Kali-Linux/Debian with proper dependancies already setup)

https://github.com/M4dmartig4n/tuya-convert

Thank you to everyone who made this possible!

-SirRedZ
