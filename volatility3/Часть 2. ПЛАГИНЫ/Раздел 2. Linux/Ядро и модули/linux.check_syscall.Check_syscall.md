```bash
vol -f ./myMachineDump.raw -s ./ linux.check_syscall.Check_syscall
```

Используется для **проверки таблицы системных вызовов** (`syscall table`) Linux на предмет наличия хуков. Хуки в системных вызовах – это механизм, позволяющий перехватывать события в операционной системе.
## Пример вывода
___
```bash
Table Address    Table Name   Index   Handler Address   Handler Symbol

0xffff81e002e0   64bit        0       0xffff876da320    __x64_sys_read
0xffff81e002e0   64bit        1       0xffff876da440    __x64_sys_write
<…>
0xffff81e002e0   64bit        36      0xffff87535480    __x64_sys_getitimer
0xffff81e002e0   64bit        39      0xffff875358c0    __x64_sys_alarm
```
## Назначение вывода
___
1.     **Модификация системных вызовов.** Некоторое вредоносное ПО может изменять syscall для перехвата и модификации поведения операционной системы.
2.    **Присутствие rootkits.** Многие rootkits используют модификацию syscall для скрытия своего присутствия от системы безопасности.