```bash
vol -f ./myMachineDump.raw -s ./ linux.bash.Bash
```
[[volatility3/Часть 2. ПЛАГИНЫ/Раздел 2. Linux/Специфические команды плагинов#! linux.bash.Bash]]

Предназначен для анализа оперативной памяти Linux-систем с целью **извлечения истории команд**, выполненных в оболочке Bash.
## Пример вывода
___
```bash
Pid   Name   Command Time                  Command

123   bash   2023-10-01 12:34:56 UTC+0000  ls -la
124   bash   2023-10-01 12:35:01 UTC+0000  pwd
125   bash   2023-10-01 12:35:05 UTC+0000  uname -a
```
