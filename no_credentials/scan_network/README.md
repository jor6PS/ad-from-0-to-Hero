# ESCANEO DE RED

```
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

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/scan_network/vid.gif?raw=true "Escaneando la red con Nmap")
