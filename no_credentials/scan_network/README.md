# ESCANEO DE RED SMB y NMAP

```Bash
#Con Crackmapexec, instalado desde el repositorio de github
poetry run crackmapexec smb <rango ip>

#Nmap ping scan
nmap -sP <rango ip>

#Nmap escaneo rápido
nmap -Pn -sV --top-ports 50 --open <rango ip>

#Nmap smb vulns
nmap -Pn --script smb-vuln* -p139,445 <rango ip>

#Nmap escaneo clasico
nmap -Pn -sC -sV -oA <output> <ranog ip>

#Nmap escaneo full
nmap -Pn -p- -sC -sV -oA <output> <ranog ip>
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/scan_network/vid.gif?raw=true "Escaneando la red con crackma y Nmap")

# ESCANEO DE RED ICMP-SCAN

```Bash
# Herramienta de escaneo ICMP con soporte multi hilo, guarda el resultao en un txt
python icm-scan.py -r <rango ip> -t <hilos>
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/scan_network/vid2.gif?raw=true "Escaneando la red con icmp-scan")

# Obteniendo hosts y servicios abiertos con escaneo pasivo con Netdiscover

```Bash
netdiscover -i <interfaz de red>
```

# Obteniendo servicios web con EyeWitness

```Bash
# Instalar EyeWitness desde su repositorio de Github: https://github.com/RedSiege/EyeWitness
python EyeWitness.py -f <filename> --timeout <optionaltimeout>
python EyeWitness.py -x <xml nmap>
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/scan_network/vid3.gif?raw=true "EyeWitness")
