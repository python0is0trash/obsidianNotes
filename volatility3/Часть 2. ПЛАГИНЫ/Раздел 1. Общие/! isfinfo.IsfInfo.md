```bash
vol -s ./ isfinfo.IsfInfo
```
[[volatility3/Часть 2. ПЛАГИНЫ/Раздел 2. Linux/Специфические команды плагинов#! isfinfo.IsfInfo]]

Предоставляет **информацию о файлах ISF** (*Intermediate Symbol Format*), которые используются для хранения символов ядра и других данных, необходимых для анализа дампа памяти. Эти файлы содержат информацию о структурах данных, типах, символах и других элементах, которые Volatility использует для интерпретации данных в памяти.
## Пример вывода
___
```bash
URI                                                            Valid    Number of base_types  Number of types  Number of symbols  Number of enums  Identifying information

file:///home/kali/Downloads/forLabWorks/isfFileMyMachine.json  Unknown  19                    11646            227021             2127             b'Linux version 6.11.2-amd64 (debian-kernel@lists.debian.org) (x86_64-linux-gnu-gcc-14 (Debian 14.2.0-6) 14.2.0, GNU ld (GNU Binutils for Debian) 2.43.1) #1 SMP PREEMPT_DYNAMIC Debian 6.11.2-1 (2024-10-05)\n\x00'
| file:///home/kali/Downloads/forLabWorks/isfFile.json         Unknown  18                    8877             143295             1529             b'Linux version 5.10.0-20-amd64 (debian-kernel@lists.debian.org) (gcc-10 (Debian 10.2.1-6) 10.2.1 20210110, GNU ld (GNU Binutils for Debian) 2.35.2) #1 SMP Debian 5.10.158-2 (2022-12-13)\n\x00'
```
## Что означает вывод
___
1.    **URI.** Путь к файлу ISF.
2.    **Valid.** Указывает, является ли файл ISF валидным. В вышеприведенном случае Unknown означает, что Volatility не смог автоматически определить валидность файла.
3.    **Number of base_types.** Количество базовых типов данных в файле ISF (базовые типы данных – это фундаментальные типы, которые используются для описания более сложных структур. Примеры базовых типов: int, char, long, pointer, struct, union и т.д.).
4.    **Number of types.** Общее количество типов данных (всевозможные типы, которые используются в ядре, включая базовые типы, структуры, объединения, массивы и т.д.).
5.    **Number of symbols.** Общее количество символов (имен функций, переменных, констант и других элементов, которые используются в ядре.).
6.    **Number of enums.** Количество перечислений (enum).
7.    **Identifying information.** Информация, которая идентифицирует ядро, например, строка баннера ядра.