```bash
vol -f ./myMachineDump.raw -s ./ linux.netfilter.Netfilter
```

Используется для **анализа цепочки Netfilter в ядре Linux**. Netfilter - это фреймворк в ядре Linux, который обеспечивает функциональность фильтрации пакетов, трансляции сетевых адресов (NAT) и других операций с сетевыми пакетами.
## Пример вывода
___
```bash
Net NS       Proto   Hook          Priority   Handler         Module                     Is Hooked

4026535992   IPV4    POST_ROUTING  -225       0xffff8780bc40  [apparmor_ipv4_postroute]  False
4026535992   IPV6    POST_ROUTING  -225       0xffff8780bbd0  [apparmor_ipv6_postroute]  False
```
## Что значит вывод
---
1. **Net NS:** Идентификатор сетевого пространства имён (Network Namespace).
2. **Proto:** Протокол (например, IPV4, IPV6).
3. **Hook:** Тип хука (например, POST_ROUTING, PRE_ROUTING, INPUT, OUTPUT, FORWARD).
4. **Priority:** Приоритет хука.
5. **Handler:** Адрес функции-обработчика.
6. **Module:** Модуль ядра, который зарегистрировал хук.
7. **Is Hooked:** Указывает, был ли хук перехвачен (True или False).
## Назначение вывода
___
1. **Обнаружение руткитов.** Руткиты часто перехватывают хуки Netfilter для скрытия своей активности или перехвата сетевого трафика. Плагин помогает выявить такие модификации.
2. **Анализ сетевой активности.** Плагин позволяет определить, какие модули и функции обрабатывают сетевые пакеты, что полезно для анализа сетевой активности системы.