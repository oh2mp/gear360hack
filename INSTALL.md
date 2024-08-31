# Installation

1. Download `gear360hack.zip` from this repository.
2. Format the memory card in camera. If you format it with a computer, choose FAT32 (vfat) and make directory DCIM onto the card.
3. Unzip the zip to the root directory of the memory card
4. Insert the card into the camera and power it up
5. Wait until it flashes the leds and shuts down

Then you are ready to go.

Note that you _must_ have files `info.tg` and `nx_cs.adj` on the card. Otherwise the hack doesn't start. If you format the card later or use a different card, remember to add those files. There is the `bootfiles.zip` included in this repository, even the installer puts right ones to the card.

By default this hack starts httpd, ftpd and telnetd (busybox versions) in the camera. 
If you want to leave eg. ftp and/or telnet away, then edit `startup.sh` first before installing.
Don't remove httpd.

Default startup.sh
```
#!/bin/sh

# Remove or comment out next line to disable ftp
/opt/usr/bin/tcpsvd -vE 0.0.0.0 21 ftpd -w /sdcard &
# Remove or comment out next line to disable telnet
LD_LIBRARY_PATH=/opt/usr/lib /opt/usr/bin/telnetd &

# This is vital. Do not touch unless you really know what you are doing.
LD_LIBRARY_PATH=/opt/usr/lib PERL5LIB=/opt/usr/lib/perl /opt/usr/bin/httpd -p 8000 -f -h /opt/usr/www &

```
The port is 8000 because the internal OSC API has reserved the port 80 and we can't use it.

Then read [USAGE.md](USAGE.md) and enjoy.
