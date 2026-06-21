# Force Citrix Workspace To Use System Certificates
```
# Citrix workspace by default comes with a set of certificates, and it doesn't use the certificates preinstalled on the system
# this sometimes might result in according to citrix workspace a missing certificate and a failed connection
# This code makes the citrix workspace aquinted with certificates installed on the system
ln -s /usr/share/ca-certificates/mozilla/* /opt/Citrix/ICAClient/keystore/cacerts/
c_rehash /opt/Citrix/ICAClient/keystore/cacerts

# Lines below might be not needed
#ln -s /etc/ssl/certs/USERTrust_RSA_Certification_Authority.pem /opt/Citrix/ICAClient/keystore/cacerts/USERTrust_RSA_Certification_Authority.pem
#cp /etc/ssl/certs/USERTrust_RSA_Certification_Authority.pem /opt/Citrix/ICAClient/keystore/cacerts
```
See fixCitrixCertificate script.
# More Details and Config
Arch Linux Wiki: https://wiki.archlinux.org/title/Citrix

# Make Self-Service (Workspace) App Work on Ubuntu 24.04
_Don't use instructions from the Citrix website, as it breaks network mounts accessible through GNOME Files (Nautilus)_
```
sudo apt-add-repository deb http://us.archive.ubuntu.com/ubuntu jammy main
sudo apt install libwebkit2gtk-4.0-dev
sudo apt-add-repository -r deb http://us.archive.ubuntu.com/ubuntu jammy main
```
_Sources:_
* https://docs.citrix.com/en-us/citrix-workspace-app-for-linux/system-requirements.html
* https://www.chippiko.com/installing-libwebkit2gtk-4-0-ubuntu

# Self-Service (Workspace) App on Debian Trixie
## Create Ubuntu 22.04 container
```
sudo apt update
sudo apt install distrobox podman -y
distrobox create --name citrix-gui --image ubuntu:22.04 --unshare-netns --additional-flags "--env DISPLAY=$DISPLAY --env XAUTHORITY=$XAUTHORITY"
```
## Download Citrix Workspace Client
Navigate to citrix page to download correct .deb package.
## Enter the Container
```
distrobox enter citrix-gui
```
Inside the container:
```
sudo apt update
sudo apt install libwebkit2gtk-4.0-37 libjavascriptcoregtk-4.0-18 libxml2 libcanberra-gtk-module pcscd libpcsclite1 libpcsclite-dev -y
sudo apt install ~/Downloads/icaclient_*_amd64.deb -y # for raspberry pi chose arm64 instead amd64
sudo ln -s /usr/share/ca-certificates/mozilla/* /opt/Citrix/ICAClient/keystore/cacerts/
sudo c_rehash /opt/Citrix/ICAClient/keystore/cacerts
distrobox-export --app selfservice
exit
```
## Run Citrix Workspace 
In your apps on the host you will see the installed app.
*Note:* _on raspberry pi you might need to run the below command after every boot_
```
xhost +si:localuser:$USER
```

# Make Mouse Middle Click Open New Tabs
You place it into ```All_Regions.ini``` config file, usually found in ```/etc/icaclient/config/All_Regions.ini```
```
[Virtual Channels\Mouse]
ClientMouseDoubleClickDetect=*
MouseTimer=*
MouseMap=
MouseXButtonMapping=
MouseWheelMapping=
MouseScrollAmount=*
MouseSendsControlV=False
PointerClickTime=*
PointerGrabTime=*
RelativeMouse=*
RelativeMousePointerFeedback=*
RelativemouseOnChar=
RelativeMouseOnShift=
RelativeMouseOffChar=
RelativeMouseOffShift=
SoftwareMouse=*
```

# Code to Ignore Disconnect Errors
You update it in ```.ICAClient/wfclient.ini```
```
[WFClient]
IgnoreErrors=9,15,32

```
