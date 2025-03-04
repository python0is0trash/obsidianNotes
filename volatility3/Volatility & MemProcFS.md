```bash
# установка зависимостей для MFTScan
pip install yara-python
vol -f ../vol3/win/2-win-memdmp/day3/MemLabs-Lab5/MemoryDump_Lab5.raw windows.mftscan.MFTScan

# установка MemProcFS
mkdir memProcFS && cd memProcFS
wget https://github.com/ufrisk/MemProcFS/releases/download/v5.14/MemProcFS_files_and_binaries_v5.14.3-linux_x64-20250212.tar.gz
tar -xvf ./MemProcFS_files_and_binaries_v5.14.3-linux_x64-20250212.tar.gz
./memprocfs

dos2unix ../vol3/win/helpVolWin # прочитать

./memprocfs -f ../vol3/win/2-win-memdmp/day3/MemLabs-Lab5/MemoryDump_Lab5.raw -forensic 1 -mount results/


```

netstat - активные на текущий момент
netscan - хз

### Плагины
---
`windows.amcache.Amcache:`
- Анализирует данные из Amcache.hve, который содержит информацию об установленных программах и исполняемых файлах.
- Полезен для: определения установленных программ, времени их установки и запуска.
---
`windows.cmdline.CmdLine:`
- Извлекает командные строки запущенных процессов.
- Полезен для: анализа команд, которые выполнялись в системе.
---
`windows.cmdscan.CmdScan:`
- Ищет в памяти фрагменты командных строк.
- Полезен для: восстановления команд, которые выполнялись в системе.
---
`windows.filescan.FileScan:`
- Сканирует память на наличие ссылок на файлы.
- Полезен для: поиска файлов, которые были открыты или удалены.
---
`windows.handles.Handles:`
- Показывает открытые дескрипторы (handles) процессов.
- Полезен для: анализа ресурсов, к которым обращались процессы (файлы, ключи реестра и т.д.).
---
`windows.info.Info:`
- Извлекает базовую информацию о системе, такую как версия ОС, имя машины и т.д.
- Полезен для: определения версии Windows и другой системной информации.
---
`windows.malfind.Malfind:`
- Ищет в памяти процессы с подозрительными характеристиками (например, внедрённый код).
- Полезен для: обнаружения вредоносных процессов.
---
`windows.netscan.NetScan:`
- Сканирует память на наличие сетевых соединений.
- Полезен для: анализа сетевой активности (IP-адреса, порты и т.д.).
---
`windows.netstat.NetStat:`
- Показывает активные сетевые соединения.
- Полезен для: анализа сетевой активности.
---
`windows.mftscan.MFTScan:`
- Сканирует память на наличие записей MFT (Master File Table).
- Полезен для: восстановления информации о файлах.
---
`windows.pslist.PsList:`
- Показывает список активных процессов.
- Полезен для: анализа запущенных процессов.
---
`windows.psscan.PsScan:`
- Ищет скрытые или завершённые процессы.
- Полезен для: обнаружения скрытых процессов.
---
`windows.pstree.PsTree:`
- Показывает дерево процессов.
- Полезен для: анализа родительско-дочерних отношений процессов.
---
`windows.psxview.PsXView:`
- Сравнивает процессы из разных источников (например, PsList, PsScan).
- Полезен для: обнаружения скрытых процессов.
---
`windows.registry.hivelist.HiveList:`
- Показывает список кустов реестра в памяти.
- Полезен для: анализа реестра.
---
`windows.registry.hivescan.HiveScan:`
- Сканирует память на наличие кустов реестра.
- Полезен для: поиска кустов реестра.
---
`windows.registry.userassist.UserAssist:`
- Анализирует ключи UserAssist, которые хранят информацию о запущенных программах.
- Полезен для: анализа активности пользователя.
---
`windows.scheduled_tasks.ScheduledTasks:`
- Показывает запланированные задачи.
- Полезен для: анализа автозагрузки и запланированных задач.
---
`windows.shimcachemem.ShimcacheMem:`
- Анализирует кэш Shimcache, который хранит информацию о запущенных программах.
- Полезен для: анализа истории запуска программ.
---
`windows.svcscan.SvcScan:`
- Показывает список сервисов.
- Полезен для: анализа сервисов Windows.
---
`windows.thrdscan.ThrdScan:`
- Ищет потоки (threads) в памяти.
- Полезен для: анализа потоков процессов.
---
`windows.vadinfo.VadInfo:`
- Показывает информацию о VAD (Virtual Address Descriptor) для процессов.
- Полезен для: анализа памяти процессов.
---
`windows.virtmap.VirtMap:`
- Показывает виртуальную карту памяти.
- Полезен для: анализа памяти.

### Вопросы
#### 1. какая версия Windows установлена (какой  Build number)? - win10 19041
```bash title:info.Info
Volatility 3 Framework 2.11.0

Variable        Value

Kernel Base     0xf80522400000
DTB     0x1aa000
Symbols file:///root/dfir-venv/lib/python3.12/site-packages/volatility3/symbols/windows/ntkrnlmp.pdb/47114209A62F3B9930F6B8998DFD4A99-1.json.xz
Is64Bit True
IsPAE   False
layer_name      0 WindowsIntel32e
memory_layer    1 FileLayer
KdVersionBlock  0xf8052300f378
Major/Minor     15.19041
MachineType     34404
KeNumberProcessors      8
SystemTime      2025-02-13 20:00:02+00:00
NtSystemRoot    C:\Windows
NtProductType   NtProductWinNt
NtMajorVersion  10
NtMinorVersion  0
PE MajorOperatingSystemVersion  10
PE MinorOperatingSystemVersion  0
PE Machine      34404
PE TimeDateStamp        Sat Apr  7 12:04:17 2068

```

> 1. Каждая версия Windows имеет свой Major номер:
> 	Windows 7: **6**
> 	Windows 8: **6**
> 	Windows 8.1: **6**
> 	Windows 10: **10** (*ранние версии*) или **15** (начиная с *Windows 10 версии 2004* и выше).
> 	Windows 11: **15** (так как Windows 11 использует то же ядро, что и Windows 10).
> 2. Minor:
> 	Дополнительный номер версии ядра. В данном случае 19041 указывает на конкретный Build Number (сборку) Windows.
> 	Например, 19041 соответствует **Windows 10 версии 2004** (May 2020 Update).
#### 2. Какое имя машины? - DESKTOP-92HHL84
user (пользователь)
```bash title:windows.registry.printkey.PrintKey+windows.registry.hivelist.HiveList
2025-02-06 16:48:54.000000 UTC  0xc28d09089000  REG_SZ  \REGISTRY\MACHINE\SYSTEM\ControlSet001\Control\ComputerName\ComputerName        (Default)       "mnmsrvc"       False
2025-02-06 16:48:54.000000 UTC  0xc28d09089000  REG_SZ  \REGISTRY\MACHINE\SYSTEM\ControlSet001\Control\ComputerName\ComputerName        ComputerName    "DESKTOP-92HHL84"       False
```
#### 3. К какому серверу пытался подключиться пользователь? под каким именем (вида user@server)?

#### 4. имя фaйna, который был удален злоумышленником

#### 5. какой пароль  от сайта gosuslugi.ru был сохранен в файле с паролями?

#### 6. имя файла, повлекшего выполнение вредоносного кода

#### 7. полный адрес, откуда был скачан данный файл

#### 8. имя процесса, в котором находится вредоносный код

#### 9. полный путь до фaмла, с помощью которого ВПО закрепилось в системе (в автозагрузке)

