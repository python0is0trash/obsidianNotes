```bash
vol -f ./myMachineDump.raw -s ./ linux.ebpf.EBPF
```

Используется для **анализа программ eBPF** (*Extended Berkeley Packet Filter*), которые запускаются в ядре Linux. eBPF – это мощная технология, позволяющая выполнять код внутри ядра и обрабатывать различные события, такие как системные вызовы или сетевые пакеты.
## Пример вывода
___
```bash
Address Name    Tag                Type

0xb27e400ed000  47dd357395126b0c   BPF_PROG_TYPE_CGROUP_DEVICE
0xb27e400fd000  6deef7357e7b4530   BPF_PROG_TYPE_CGROUP_SKB
0xb27e401a9000  6deef7357e7b4530   BPF_PROG_TYPE_CGROUP_SKB
0xb27e401af000  ee0e253c78993a24   BPF_PROG_TYPE_CGROUP_DEVICE
```
