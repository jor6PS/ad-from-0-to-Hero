# List null y anonymous access and shares

```BAsh
#Crackmapexec enumera null sesions
poetry run crackmapexec smb <rango ip> -u '' -p ''

#Crackmapexec enumera sesiones anonimas
poetry run crackmapexec smb <rango ip> -u 'a' -p ''

#Para obtener carpetas compartidas con acceso libre incluir --shares al final
poetry run crackmapexec smb <rango ip> -u '' -p '' --shares
poetry run crackmapexec smb <rango ip> -u 'a' -p '' --shares
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/list_guest_access_on_smb_share/files/vid.gif?raw=true "Enumerando sesiones nulas ya anonimas con crackmapexec")

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/list_guest_access_on_smb_share/files/vid2.gif?raw=true "Obteniendo los shares abiertos sin auteniticacion con crackmapexec")

# Enumerando usuarios full, enum4linux-ng

```Bash
enum4linux-ng.py -As <target> -oY <output> -t <timeout en segundos>
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/list_guest_access_on_smb_share/files/vid3.gif?raw=true "Enumerando usuarios full")
