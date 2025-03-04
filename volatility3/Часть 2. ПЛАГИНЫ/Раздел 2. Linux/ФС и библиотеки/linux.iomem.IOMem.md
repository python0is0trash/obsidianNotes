```bash
vol -f ./myMachineDump.raw -s ./ linux.iomem.IOMem
```

Используется для **анализа и вывода информации о карте памяти системы Linux**, подобно тому, что можно увидеть в `/proc/iomem`. Этот плагин помогает выявить различные области памяти, зарезервированные для системных компонентов, таких как RAM, PCI-устройства и другие аппаратные ресурсы.
## Пример вывода
___
```bash
Name                     Start        End

PCI mem                  0x0          0xffffffffff
* Reserved               0x0          0xffd
* System RAM             0x2000       0x9fdff
** System ROM            0xd0000      0xffaff
**** virtio-pci-modern   0xfff00000   0xfaa03fff
```
