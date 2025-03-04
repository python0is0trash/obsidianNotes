```bash
vol -f ./myMachineDump.raw -s ./ linux.envars.Envars
```
[[volatility3/Часть 2. ПЛАГИНЫ/Раздел 2. Linux/Специфические команды плагинов#! linux.envars.Envars / ! linux.malfind.Malfind]]

Используется для **извлечения и анализа переменных окружения** (*envars*) **процессов** Linux из дампа памяти.
## Пример вывода
___
```bash
PID    PPID    COMM           KEY             VALUE

1      0       systemd        HOME            /
215    1       systemd-udevd  LISTEN_FDNAMES  systemd-udevd-control.socket:systemd-udevd-kernel.socket
373    1       cron           PATH            /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```
## Что означает вывод
___

## Назначение вывода
___
1.    **Анализ поведения процессов.** Вывод позволяет увидеть все используемые процессы и их конфигурацию через переменные среды.
2.    **Обнаружение вредоносной активности.** Если обнаружены подозрительные значения в переменных среды (например, пути к неизвестным библиотекам), это может указывать на присутствие вредоносного ПО.