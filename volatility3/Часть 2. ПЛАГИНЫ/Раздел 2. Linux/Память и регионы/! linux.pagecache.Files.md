```bash
vol -f ./myMachineDump.raw -s ./ linux.pagecache.Files
```
[[volatility3/Часть 2. ПЛАГИНЫ/Раздел 2. Linux/Специфические команды плагинов#! linux.pagecache.Files]]

Используется для **анализа файлов, которые находятся в кэше страниц** (`page cache`) ядра Linux. Кэш страниц - это механизм ядра, который хранит данные файлов в оперативной памяти для ускорения доступа к ним. Этот плагин позволяет определить, какие файлы и их части находятся в кэше.
## Пример вывода
___
```bash
SuperblockAddr  MountPoint  Device  InodeNum   InodeAddr       FileType  InodePages   CachedPages   FileMode        AccessTime  ModificationTime  ChangeTime   FilePath

0xa0bf8104a800  /           0:2     1          0xa0bf81414e40  DIR       0            0             drwxr-xr-x      date UTC    date UTC          date UTC     /
0xa0bf81d8f800  /sys        0:19    16577      0xa0bf866a8be0  LNK       0            0             lrwxrwxrwx      date UTC    date UTC          date UTC     /sys/block/sda
0xa0bf81d8f800  /sys        0:19    8240       0xa0bf865ef560  LNK       0            0             lrwxrwxrwx      date UTC    date UTC          date UTC     /sys/class/tty/tty49
0xa0bf81d8f800  /sys        0:19    769        0xa0bf865c4720  DIR       0            0             drwxr-xr-x      date UTC    date UTC          date UTC     /sys/class/master
```
## Что значит вывод
---
1. **SuperblockAddr:** Адрес суперблока, связанного с файлом.
2. **MountPoint:** Точка монтирования, к которой относится файл.
3. **Device:** Устройство, на котором находится файл (в формате MAJOR:MINOR).
4. **InodeNum:** Номер inode файла.
5. **InodeAddr:** Адрес inode в памяти.
6. **FileType:** Тип файла (например, DIR - каталог, LNK - символическая ссылка, REG - регулярный файл).
7. **InodePages:** Количество страниц, связанных с inode.
8. **CachedPages:** Количество страниц файла, находящихся в кэше.
9. **FileMode:** Права доступа к файлу (например, drwxr-xr-x для каталога, lrwxrwxrwx для символической ссылки).
10. **AccessTime:** Время последнего доступа к файлу.
11. **ModificationTime:** Время последнего изменения файла.
12. **ChangeTime:** Время последнего изменения метаданных файла.
13. **FilePath:** Полный путь к файлу.
## Назначение вывода
___
**Анализ активности файловой системы.** Плагин позволяет определить, какие файлы и их части активно использовались системой на момент создания дампа памяти.
**Поиск подозрительных файлов.** Если в кэше страниц находятся подозрительные файлы (например, с необычными именами или путями), это может указывать на вредоносную активность.