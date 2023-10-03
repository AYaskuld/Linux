## Runlevels

"Runlevel" определяет состояние компьютера после загрузки.

В стандартной практике, когда компьютер переходит на нулевой уровень выполнения, он останавливается, а когда он переходит на шестой уровень выполнения, он перезагружается. Уровни выполнения по умолчанию обычно равны 3, 4 или 5. Более низкие уровни запуска полезны для технического обслуживания или аварийного ремонта, поскольку они обычно вообще не предлагают никаких сетевых услуг. 

- /etc/rc[0-6].d/
- K20nfs -> ../init.d/nfs
- S10network -> ../init.d/network
- /etc/inittab id:3:initdefault:

<img src ="https://elearn.epam.com/assets/courseware/v1/a2f48b39806dfd4e3075563f42c03e9d/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/runlevels.png">

### Systemd runlevels

In systemd runlevels are referred to as targets.

- Run level 0 is matched by poweroff.target (and runlevel0.target is a symbolic link to poweroff.target).
- Run level 1 is matched by rescue.target (and runlevel1.target is a symbolic link to rescue.target).
- Run level 3 is emulated by multi-user.target (and runlevel3.target is a symbolic link to multi-user.target).
- Run level 5 is emulated by graphical.target (and runlevel5.target is a symbolic link to graphical.target).
- Run level 6 is emulated by reboot.target (and runlevel6.target is a symbolic link to reboot.target).
- Emergency is matched by emergency.target.

View default runlevel:

    $ systemctl get-default

Set default runlevel:

    $ systemctl set-default runlevel0.target
