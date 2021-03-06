# USB-buffer
A buffer between an unreliable USB key and your computer (to download files from the key to the PC)

Does this make sense?

Material: Raspberry Pi 4, ethernet cable, PC

1. Burn Raspbian on an SD card using Raspberry Pi Imager
2. Connect to it 
 - note: for headless connection: 
 a) create an empty file called "ssh" at the root of the SD card
 b) using an ethernet cable + Putty: connect to pi.local on port 22 - password raspberry
3. change the default password using passwd
4. you might want to implement additional security measures (firewall, changing SSH default port, ...)
5. sudo raspi-config -> Wireless LAN -> Set up country
6. connect through internet either through a Wifi access point or through the ethernet cable (you might want to share the internet connection of your computer)

7.
````
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install usbmount apache2
````
8. you might want to increase the security by configuring https, passwords, etc.

9.
````
    sudo vim /lib/systemd/system/systemd-udevd.service
    PrivateMounts=no
    Verify that noexec is set as a mount option
````

10. config the pi as an access point according to https://www.raspberrypi.org/documentation/configuration/wireless/access-point-routed.md

11.
````
    cd /var/www/html
    
    sudo ln -s /media/usb0 usb0
    sudo ln -s /media/usb1 usb1
    sudo ln -s /media/usb2 usb2
    sudo ln -s /media/usb3 usb3
    
````

12. plug your USB key in your Rpi
13. connect your computer to the Rpi through Wifi
14. in your browser, go to http://raspberry.local and download the files you want

You might also connect through SFTP (eg using FileZilla)
