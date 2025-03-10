```bash
vol -f ./myMachineDump.raw banners.Banners
```

Содержит информацию о строках **баннеров ядра Linux**, которые были найдены в дампе памяти. Эти строки обычно содержат информацию о:
- версии ядра,
- компиляторе,
- дате сборки и других деталях, связанных с операционной системой.
## Пример вывода
___

```bash
Offset         Banner

0xb48000e0     Linux version 6.11.2-amd64** (devel@kali.org) (x86_64-linux-gnu-gcc-14 (Debian 14.2.0-6) 14.2.0, GNU ld (GNU Binutils for Debian) 2.43.1) # SMP PREEMPT_DYNAMIC Kali 6.11.2-1kali1 (2024-10-15)
0xb4989d00     Linux version 6.11.2-amd64 (devel@kali.org) (x86_64-linux-gnu-gcc-14 (Debian 14.2.0-6) 14.2.0, GNU ld (GNU Binutils for Debian) 2.43.1) #1 SMP PREEMPT_DYNAMIC Kali 6.11.2-1kali1 (2024-10-15)
0xb5f61ee0     Linux version 6.11.2-amd64 (devel@kali.org) (x86_64-linux-gnu-gcc-14 (Debian 14.2.0-6) 14.2.0, GNU ld (GNU Binutils for Debian) 2.43.1) #1 SMP PREEMPT_DYNAMIC Kali 6.11.2-1kali1 (2024-10-15)5)
```
## Что означает вывод
___
1.     Linux version 6.11.2-amd64:
	- версия ядра Linux: 6.11.2.
	- архитектура: amd64 (64-битная).
2.    (devel@kali.org) - электронная почта или идентификатор разработчика/команды, собравшей ядро.
3.    (x86_64-linux-gnu-gcc-14 (Debian 14.2.0-6) 14.2.0, GNU ld (GNU Binutils for Debian) 2.43.1) - информация о компиляторе и линкере:
	- компилятор: gcc-14 версии 14.2.0.
	- линкер: GNU ld версии 2.43.1.
4.    # SMP PREEMPT_DYNAMIC - тип ядра:
	- SMP (Symmetric Multi-Processing) — поддержка многопроцессорных систем.
	- PREEMPT_DYNAMIC — тип планировщика ядра, поддерживающий вытесняющую многозадачность.
5.    Kali 6.11.2-1kali1 (2024-10-15) - дистрибутив и версия пакета ядра:
	- дистрибутив: Kali.
	- версия пакета: 6.11.2-1kali1.
	- дата сборки: 2024-10-15.
## Назначение вывода
___
1.    **Определение версии ядра.** Возможно точно определить версию ядра, которая использовалась в системе на момент создания дампа памяти.
2.    **Выбор профиля Volatility2.** Зная версию ядра и дистрибутив, вы можете выбрать правильный профиль для анализа дампа памяти. Например, если основная версия ядра - 6.11.2-amd64, можно использовать профиль Volatility, соответствующий этой версии:
```bash
volatility -f <memory_dump> --profile=LinuxKali6_11_2x64 <other_plugins>
```
3.    **Анализ окружения.** Информация о компиляторе и дате сборки может быть полезна для понимания окружения, в котором работала система.
4.    **Обнаружение аномалий.** Если в системе обнаружены баннеры от разных версий ядра, это может указывать на необычные события, такие как обновление ядра или наличие следов взлома.