[From this Google search](https://www.google.com/search?client=firefox-b&q=set+GPIO+pullup+from+bash):
[Then, from this page:](https://raspberrypi-aa.github.io/session2/bash.html)
[Perhaps a better search result:](https://duckduckgo.com/?q=set+GPIO+pullup+from+bash&t=ffnt&ia=web)
[be sure to read this for background:](https://luketopia.net/2013/07/28/raspberry-pi-gpio-via-the-shell/)
[and esp. read this for background:](https://iqjar.com/jar/programming-the-raspberry-pis-gpio-pins-from-command-line-and-bash-script/)
[and esp. esp. read this one, as this guy is the author of gpio](https://projects.drogon.net/raspberry-pi/wiringpi/the-gpio-utility/)

Using GPIO from bash

The following commands should be run as root (type 'sudo bash' to become root). This code sets up pin 18 to be an output, 
sets the pin high and then sets it low.

#   Exports pin to userspace
echo "18" > /sys/class/gpio/export                  

# Sets pin 18 as an output
echo "out" > /sys/class/gpio/gpio18/direction

# Sets pin 18 to high
echo "1" > /sys/class/gpio/gpio18/value

# Sets pin 18 to low
echo "0" > /sys/class/gpio/gpio18/value 

This next snippet sets up pin 4 to be an input, then reads the value of the input.

echo "4" > /sys/class/gpio/export
echo "in" > /sys/class/gpio/gpio4/direction
cat /sys/class/gpio/gpio4/value

---------

root@raspberrypi3b:/home/pi# ls -l /sys/devices/platform/soc/3f200000.gpio/gpiochip0/gpio/gpio4
total 0
-rwxrwx--- 1 root gpio 4096 Jan 26 22:39 active_low
lrwxrwxrwx 1 root gpio    0 Jan 26 22:39 device -> ../../../gpiochip0
-rwxrwx--- 1 root gpio 4096 Jan 26 22:41 direction
-rwxrwx--- 1 root gpio 4096 Jan 26 22:39 edge
drwxrwx--- 2 root gpio    0 Jan 26 22:39 power
lrwxrwxrwx 1 root gpio    0 Jan 26 22:39 subsystem -> ../../../../../../../class/gpio
-rwxrwx--- 1 root gpio 4096 Jan 26 22:39 uevent
-rwxrwx--- 1 root gpio 4096 Jan 26 22:39 value
root@raspberrypi3b:/home/pi# cat /sys/devices/platform/soc/3f200000.gpio/gpiochip0/gpio/gpio4/direction
in
root@raspberrypi3b:/home/pi# cat /sys/devices/platform/soc/3f200000.gpio/gpiochip0/gpio/gpio4/active_low
0
root@raspberrypi3b:/home/pi# echo "1" > /sys/class/gpio/gpio4/active_low
root@raspberrypi3b:/home/pi# cat /sys/devices/platform/soc/3f200000.gpio/gpiochip0/gpio/gpio4/active_low
1
root@raspberrypi3b:/home/pi# 