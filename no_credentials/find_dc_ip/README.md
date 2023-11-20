# Enseñando la ip del DC

```Bash
nslookup -type=SRV _ldap._tcp.dc._msdcs.<nombre dominio completo> <rango ip>
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/no_credentials/find_dc_ip/files/vid.gif?raw=true "NSlookup")
