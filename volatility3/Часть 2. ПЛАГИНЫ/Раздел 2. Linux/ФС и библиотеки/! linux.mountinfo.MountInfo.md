```bash
vol -f ./myMachineDump.raw -s ./ linux.mountinfo.MountInfo
```
[[volatility3/Часть 2. ПЛАГИНЫ/Раздел 2. Linux/Специфические команды плагинов#! linux.mountinfo.MountInfo]]

Используется для вывода **информации о смонтированных файловых системах** в Linux-системе.
## Пример вывода
___
```bash
MNT_NS_ID    MOUNT ID  PARENT_ID   MAJOR:MINOR  ROOT                   MOUNT_POINT     MOUNT_OPTIONS                   FIELDS      FSTYPE    MOUNT_SRC   SB_OPTIONS

4026431840   1         1           0:2          /                      /               rw                              rootfs      none      rw          rw
4026431840   204       25          0:38         /                      /run/user/0     rw,nosuid,nodev,relatime        shared:119  tmpfs     tmpfs       rw
4026432212   70        68          0:25         /                      /sys/fs/cgroup  rw,nosuid,nodev,noexec,relatime shared:31   master:9  cgroup2     cgroup2 rw
4026432233   112       104         0:19         /                      /sys            ro,nosuid,nodev,noexec,relatime shared:48   master:7  sysfs       sysfs   rw
4026432233   137       104         8:1          /tmp/systemd-8c34158   /tmp            rw,relatime                     shared:75   master:1  ext4        /dev/sda1       
```
## Что означает вывод
---
1. **MNT_NS_ID:** Идентификатор пространства имён монтирования.
2. **MOUNT ID:** Уникальный идентификатор монтирования.
3. **PARENT_ID:** Идентификатор родительского монтирования.
4. **MAJOR:MINOR:** Идентификатор устройства (основной и дополнительный номера).
5. **ROOT:** Корневой каталог монтирования.
6. **MOUNT_POINT:** Точка монтирования.
7. **MOUNT_OPTIONS:** Параметры монтирования (например, rw, relatime).
8. **FIELDS:** Дополнительные поля (например, shared, private).
9. **FSTYPE:** Тип файловой системы (например, ext4, proc, sysfs).
10. **MOUNT_SRC:** Источник монтирования (например, устройство или виртуальная файловая система).
11. **SB_OPTIONS:** Параметры суперблока (например, rw, errors=remount-ro).
## Назначение вывода
___
1. **Анализ смонтированных файловых систем.** Плагин позволяет определить, какие файловые системы были смонтированы в системе на момент создания дампа памяти.
2. **Поиск подозрительных точек монтирования.** Если в системе смонтирована подозрительная файловая система (например, с необычным типом или параметрами), это может указывать на вредоносную активность.