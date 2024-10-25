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