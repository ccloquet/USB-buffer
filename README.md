# USB-buffer
A buffer between an unreliable USB key and your computer.

Does this make sense?

Material: Raspberry Pi 4

1. Burn Raspbian on an SD card using Raspberry Pi Imager
2. Connect to it 
 - note: for headless connection: 
 1. create an empty file called "ssh" at the root of the SD card
 2. using an ethernet cable + Putty: connect to pi.local on port 22 - password raspberry
3. change the default password using passwd
4. you might want to implement additional security measures (firewall, changing SSH default port, ...)
5. sudo raspi-config -> Wireless LAN -> Set up country
6. connect through internet either through a Wifi access point or through the ethernet cable (you might want to share the internet connection of your computer)

````
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install usbmount apache2
````
````
    sudo vim /lib/systemd/system/systemd-udevd.service
    PrivateMounts=no
````

10. config the pi as an access point according to https://www.raspberrypi.org/documentation/configuration/wireless/access-point-routed.md

````
    cd /var/www/html
    
    sudo ln -s /media/usb0 usb0
    sudo ln -s /media/usb1 usb1
    sudo ln -s /media/usb2 usb2
    sudo ln -s /media/usb3 usb3
    
````

11. plug your USB key in your Rpi
12. connect your computer to the Rpi through Wifi
13. in your browser, go to http://raspberry.local and download the files you want
14. you might want to increase the security by configuring https, passwords, etc.
