# Installation

1. Download `gear360hack.zip` from this repository.
2. Format the memory card in camera.
3. Unzip the zip to the root directory of the memory card
4. Insert the card into the camera and power it up
5. Wait until it flashes the leds and shuts down

After that you can remove everything from the memory card, but you _must_ leave the `DCIM` directory and files `info.tg` and `nx_cs.adj` there.
Then you are ready to go.

By default this hack starts httpd, ftp and telnet daemons in the camera. If you want to leave ftp and/or telnet away, then edit `startup.sh`first before installing.

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
