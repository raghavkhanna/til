# Persistent naming for usb-serial devices

Change /dev/ttyUSB* to something more descriptive. Eg: /dev/autopilot

1. Lookup the Vendor ID and Product ID
   ```
   lsusb
   ```
2. Lookup the attributes you want for the device
   ```
   udevadm info -a -n /dev/ttyUSB1 | grep '{serial}' | head -n1
   ```
3. Write your udev file in /etc/udev/rules.d/99-persistent-usb-serial.rules
   ```
   SUBSYSTEM=="tty", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="A6008isP", SYMLINK+="autopilot"
   ```
4. Verify if the udev rules work
   ```
   sudo udevadm test /devices/pci0000:00/0000:00:14.0/usb2/2-2/2-2:1.0/ttyUSB1/tty/ttyUSB1
   ```
   
[source1-udev-rules](http://weininger.net/how-to-write-udev-rules-for-usb-devices.html)  
[source2-serial-usb](http://hintshop.ludvig.co.nz/show/persistent-names-usb-serial-devices/)
