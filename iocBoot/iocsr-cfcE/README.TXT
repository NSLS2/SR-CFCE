EPICS & subdirectoris readable+exexutable!
cd /epics/iocs/SR-CFCA/iocBoot/iocsr-cfcA
sudo runuser -l softioc -c /epics/iocs/SR-RF/iocBoot/iocsr-cfcA/Run.sh


#!/bin/sh
cd /epics/iocs/SR-CFCA/iocBoot/iocsr-cfcA;procServ -n "SR-CFCA" -L/var/log/softioc/SR-CFCA/SR-CFCA.log -i ^D^C 4051 ./st.cmd;
date;


jtagger@rfctl64-1:/etc/udev/rules.d$ more 99-opal-kelly.rules
# Linux 2.6
#SUBSYSTEMS=="usb", ATTRS{idVendor}=="151f", OWNER="softioc", GROUP="controls"
# Linux 3.2
#SUBSYSTEM=="usb", ATTR{idVendor}=="151f", OWNER="softioc", GROUP="controls"

# Linux 2.6
SUBSYSTEMS=="usb", ATTRS{idVendor}=="151f", MODE="0666"
# Linux 3.2
SUBSYSTEM=="usb", ATTR{idVendor}=="151f", MODE="0666"


# Reminder
# udevadm info -a -p $(udevadm info -q path -n /dev/bus/usb/002/009)

jtagger@rfctl64-1:/etc/udev/rules.d$

sudo udevadm control --reload-rules
sudo udevadm trigger

cp scripts/SR-CFCA.service/etc/systemd/system/ioc.srcfcA.service /etc/systemd/system
chown root:root /etc/systemd/system/ioc.srcfcA.service

sudo ln -s /etc/systemd/system/ioc.srcfcA.service ioc.srcfcA.service

systemctl enable ioc.srcfcA
systemctl start ioc.srcfcA
systemctl status ioc.srcfcA -l
systemctl stop ioc.srcfcA
systemctl reload ioc.srcfcA

