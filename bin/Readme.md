# More Details and Config
Arch Linux Wiki: https://wiki.archlinux.org/title/Citrix

# Make Mouse Middle Click Open New Tabs
You place it into ```All_Regions.ini``` config file, usually found in ```/etc/icaclient/config```
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