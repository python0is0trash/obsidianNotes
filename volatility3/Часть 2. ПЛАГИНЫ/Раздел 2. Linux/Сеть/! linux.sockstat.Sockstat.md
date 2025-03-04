```bash
vol -f ./myMachineDump.raw -s ./ linux.sockstat.Sockstat
```
[[volatility3/Часть 2. ПЛАГИНЫ/Раздел 2. Linux/Специфические команды плагинов#! linux.sockstat.Sockstat]]

Используется для **анализа сетевых сокетов** в Linux-системах. Он выводит информацию о всех открытых сокетах, включая их тип, протокол, адреса, порты и состояние.
## Пример вывода
___
```bash
NetNS        Process Name  PID   TID   FD   Sock Offset     Family   Type     Proto  Source Addr   Source Port   Destination Addr              Destination Port  State        Filter

4026533992   systemd       1     1     54   0xa0bf830d5800  AF_UNIX  STREAM   -      -             10303         /run/dbus/system_bus_socket   10488             ESTABLISHED  -
4026533992   sd-resolve    287   372   2    0xa0bf830d5000  AF_UNIX  STREAM   -      -             10323         /run/systemd/journal/stdout   10424             ESTABLISHED  -
4026533992   qemu-ga       376   376   5    0xa0bf8344b400  AF_UNIX  DGRAM    -      -             11304         /run/systemd/journal/dev-log  10379             UNCONNECTED  -
4026533992   sshd          419   419   1    0xa0bfb3804c00  AF_UNIX  STREAM   -      -             11342         /run/systemd/journal/stdout   11470             ESTABLISHED  -
```
## Что означает вывод
___
1. **NetNS** - идентификатор сетевого пространства имён (`Network Namespace`).
2. **Process Name** - имя процесса, открывшего сокет.
3. **PID** - идентификатор процесса.
4. **TID** - идентификатор потока.
5. **FD** - файловый дескриптор сокета.
6. **Sock Offset** - смещение сокета в памяти.
7. **Family** - семейство протоколов (например, `AF_UNIX`, `AF_INET`).
8. **Type** - тип сокета (например, `STREAM`, `DGRAM`).
9. **Proto** - протокол (например, `TCP`, `UDP`, `NETLINK_KOBJECT_UEVENT`).
10. **Source Addr** - исходный IP-адрес.
11. **Source Port** - исходный порт.
12. **Destination Addr** - целевой IP-адрес.
13. **Destination Port** - целевой порт.
14. **State** - состояние сокета (например, `LISTEN`, `UNCONNECTED`).
15. **Filter** - информация о фильтрах (например, `BPF`).
## Назначение вывода
___
1. **Анализ сетевой активности.** Возможно определить, какие процессы используют сетевые сокеты и для каких целей. Например, процесс `systemd` использует UNIX-сокеты для взаимодействия с другими компонентами системы.
2. **Поиск подозрительных сокетов.** Если в системе есть сокеты с неизвестными адресами или портами, это может указывать на подозрительную активность.
3. **Исследование межпроцессного взаимодействия.** UNIX-сокеты (`AF_UNIX`) используются для IPC. Вы можете определить, какие процессы взаимодействуют друг с другом.
4. **Анализ фильтров.** Фильтры (например, `cBPF`) могут быть использованы для анализа сетевого трафика. Если фильтры настроены неправильно, это может быть признаком атаки.