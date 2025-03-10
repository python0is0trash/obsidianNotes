```bash
vol -f ./myMachineDump.raw -s ./ linux.pstree.PsTree --threads --decorate-comm
```
[[volatility3/Часть 2. ПЛАГИНЫ/Раздел 2. Linux/Специфические команды плагинов#! linux.pstree.PsTree]]

Используется для **отображения дерева процессов** в Linux-системе. Он показывает иерархию процессов, начиная с корневого процесса (обычно `systemd` или `init`), и позволяет увидеть, какие процессы были запущены другими процессами.
## Пример вывода
___
```bash
OFFSET (V)      PID     TID     PPID    COMM
```
## Что означает вывод
___
1. **OFFSET (V)** - виртуальное смещение процесса в памяти.
2. **PID** - идентификатор процесса.
3. **TID** - идентификатор потока (в Linux обычно равен `PID`, если это не многопоточный процесс).
4. **PPID** - идентификатор родительского процесса.
5. **COMM** - имя команды (исполняемого файла).
## Назначение вывода
___
см. [[! linux.pslist.PsList]]
