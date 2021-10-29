
Connect to the Raspberry Pi
```
$ ssh pi@yourraspberrylocalipaddress
```
password: raspberry

Change password:
```
$ passwd
```

-> setup local
-> time zone: 'US/Eastern'
-> change hostname to 'yourhostname'
```
$ sudo raspi-config
```

Update
```
$ sudo apt update
$ sudo apt upgrade -y
```

To avoid interface eth0 error
```
$ sudo rm -f /etc/systemd/network/99-default.link
$ sudo reboot
```

After reboot, proceed to install OpenMediaVault + Extras
```
$ sudo wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash
```
(Will reboot automatically in the end)

Set Static IP for Raspberry PI (Optional)

In your router or Modem, go to advanced settings:

In the setup menu, find LAN Setup --> 
In the Address Reservation Section add the local Ip you want to associate with your raspberry pi and the macaddress of raspberry pi( if you are connected to pi already you can see it in the  attached devices of Router)


Go to OMV dashboard
```
  Example: http://yourraspberrylocalipaddress
  username: admin
  password: openmediavault
```
Change the default password

There are setup guides for OMV in online, it's pretty straight forward.
You can follow this: https://www.youtube.com/watch?v=iNRPHOWpvTo

Once it is setup, go to OMV-Extras, install docker, restart OMV and then in OMV-Extras install portainer to manage contaienr in raspberry pi.


