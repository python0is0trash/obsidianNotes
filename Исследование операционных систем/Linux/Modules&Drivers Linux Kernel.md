### Изучение существующих модулей
---
```bash title:"Установка компонентов для работы с модулями ядра"
sudo apt-get install build-essential kmod
```

```bash title:"Просмотр существующих модулей"
sudo lsmod OR cat /proc/modules
```

### Создание и сборка модуля
---
> [!NOTE] Важно
> Предварительно нужно проверить, установлены ли исходные коды ядра командой `apt-cache search linux-headers-uname -r` (если они есть, то вам очень повезло), если их нет, то действуем по следующему алгоритму:
>```bash title:"Скачивание необходимой версии исходных кодов ядра"
>uname -r # смотрим версию ядра
>
>apt search linux-headers-'uname -r' # в выводе ищем строку с заголовком вида 'linux-headers-6.12.13-amd64'
>apt install linux-headers-'uname -r' # устанавливаем заголовок, если есть в списке вывода выше
>ls -la /lib/modules/ # Проверяем наличие заголовка в системе. Должна быть папка вида '6.12.13-amd64', и содержащая папку 'build'
>
>OR
>
># 1. скачиваем отдельно заголовок ядра .deb (linux-headers-'uname -r') вида linux-headers-6.11.2-amd64_6.11.2-1_amd64.deb
># 2. скачиваем отдельно .deb (linux-headers-'uname -r'-common) вида linux-headers-6.11.2-common_6.11.2-1_all.deb
># 3. скачиваем отдельно .deb (linux-kbuild-'uname -r') вида linux-kbuild-6.11.2_6.11.2-1_amd64.deb
># 4. распаковываем все эти пакеты, последовательно выполняя команды dpkg -i 'module'
># В результате в папке /usr/src должны появиться 3 соответствующие папки:
>#     linux-headers-6.11.2-amd64
>#     linux-headers-6.11.2-common
>#     linux-kbuild-6.11.2 -> ../lib/linux-kbuild-6.11.2
>```

```bash title:"Создание директории для работы с кодом модуля"
mkdir -p /home/kali/develop/kernel/hello-1
cd /home/kali/develop/kernel/hello-1

touch hello-1.c && touch Makefile
```

```c title:hello-1.c
/*
 * hello-1.c – простейший модуль ядра.
 */
#include <linux/kernel.h> /* необходим для pr_info() */
#include <linux/module.h> /* необходим для всех модулей */
 
int init_module(void)
{
    pr_info("Hello world 1.\n");
 
    /* Если вернётся не 0, значит, init_module провалилась; модули загрузить не получится. */
    return 0;
}
 
void cleanup_module(void)
{
    pr_info("Goodbye world 1.\n");
}
 
MODULE_LICENSE("GPL");
```

```bash title:Makefile
obj-m += hello-1.o  
  
PWD := $(CURDIR)  
  
all:  
make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules # вместо $(shell uname -r) должен быть путь типа '6.12.13-amd64', если заголовки ядра были установлены извне
  
clean:  
make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean # аналогично пункту выше
```

```bash title:"make - сборка модуля"
make -C /lib/modules/6.11.2-amd64/build M=/home/kali/develop/kernel/hello-1 modules
make[1]: Entering directory '/usr/src/linux-headers-6.11.2-amd64'
  CC [M]  /home/kali/develop/kernel/hello-1/hello-1.o
/home/kali/develop/kernel/hello-1/hello-1.o: warning: objtool: init_module(): not an indirect call target
/home/kali/develop/kernel/hello-1/hello-1.o: warning: objtool: cleanup_module(): not an indirect call target
  MODPOST /home/kali/develop/kernel/hello-1/Module.symvers
  CC [M]  /home/kali/develop/kernel/hello-1/hello-1.mod.o
  LD [M]  /home/kali/develop/kernel/hello-1/hello-1.ko
  BTF [M] /home/kali/develop/kernel/hello-1/hello-1.ko
Skipping BTF generation for /home/kali/develop/kernel/hello-1/hello-1.ko due to unavailability of vmlinux
make[1]: Leaving directory '/usr/src/linux-headers-6.11.2-amd64'
```

### Просмотр информации о модуле
---
```bash title:"# file hello-1.ko"
hello-1.ko: ELF 64-bit LSB relocatable, x86-64, version 1 (SYSV), BuildID[sha1]=1b4555238c02b3914aa267120bbfa84ffc609e3e, with debug_info, not stripped

# Модуль - исполняемый ELF-файл
```
```bash title:"# modinfo hello-1.ko"
filename:       /home/kali/develop/kernel/hello-1/hello-1.ko
license:        GPL
depends:        
retpoline:      Y
name:           hello_1
vermagic:       6.11.2-amd64 SMP preempt mod_unload modversions 

# выводит сводную информацию о модуле
```
```bash title:"Загрузка модуля в ядро и проверка работоспособности"
insmod hello-1.ko
lsmod | grep hello # просмотр существования модуля

journalctl --since "1 hour ago" | grep kernel # просмотр логов для анализа работы модуля
  # Feb 25 14:39:43 kali kernel: hello_1: disagrees about version of symbol module_layout
  # Feb 25 14:40:30 kali kernel: hello_1: disagrees about version of symbol module_layout
  # Feb 25 15:18:14 kali kernel: hello_1: loading out-of-tree module taints kernel.
  # Feb 25 15:18:14 kali kernel: hello_1: module verification failed: signature and/or required key missing - tainting kernel
  # Feb 25 15:18:14 kali kernel: Hello world 1.


rmmod hello_1 # удаление модуля из ядра
```


> [!NOTE] Полная перекомпиляция
> ```bash
rmmod hello_1
>
make clean
make
>
insmod hello-1.ko
>
journalctl --since "1 hour ago" | grep kernel
>```

