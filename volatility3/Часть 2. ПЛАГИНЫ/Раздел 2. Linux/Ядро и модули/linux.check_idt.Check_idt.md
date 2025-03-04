```bash
vol -f ./myMachineDump.raw -s ./ linux.check_idt.Check_idt
```

Используется **для проверки целостности таблицы прерываний** (`Interrupt Descriptor Table`, `IDT`) Linux. Он анализирует память и сравнивает текущие значения IDT с ожидаемыми, чтобы обнаружить потенциальные модификации.
## Пример вывода
___
```bash
Index   Address          Module      Symbol

0x0     0xffff87e008a0   __kernel__  asm_exc_divide_error
0x1     0xffff87e00b90   __kernel__  asm_exc_debug
0x2     0xffff87e014d0   __kernel__  asm_exc_nmi
0x3     0xffff87e00ab0   __kernel__  asm_exc_int3
0x4     0xffff87e008c0   __kernel__  asm_exc_overflow
0x5     0xffff87e008e0   __kernel__  asm_exc_bounds
0x6     0xffff87e00a90   __kernel__  asm_exc_invalid_op
<….>
0x80     0xffff87e018a0   __kernel__  entry_INT80_compat
```
