# VIDEO ESCANEO DE RED

Referencia vid

#COMANDOS

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