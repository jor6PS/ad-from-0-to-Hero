#Video list null y anonymous access

Referencia vid
Referencia vid2

#Comandos

```
#Crackmapexec enumera null sesions
poetry run crackmapexec smb <rango ip> -u '' -p ''

#Crackmapexec enumera sesiones anonimas
poetry run crackmapexec smb <rango ip> -u 'a' -p ''

#Para obtener carpetas compartidas con acceso libre incluir --shares al final
poetry run crackmapexec smb <rango ip> -u '' -p '' --shares
poetry run crackmapexec smb <rango ip> -u 'a' -p '' --shares
```


# Video enum4linux-ng

Referencia vid3

#Comandos

```
enum4linux-ng.py -As <target> -oY <output>
```
