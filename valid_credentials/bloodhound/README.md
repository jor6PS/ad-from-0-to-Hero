# BLOODHOuND

```
# Query para extraer la información del AD (primero incluir el DNS en la configuración de red). Obtener el script de Github: https://github.com/dirkjanm/BloodHound.py
python bloodhound.py --zip -c All -d <nombre completo de dominio> -u <user>@<nombre completo de dominio> -p <cpass> -dc <nombre dns del DC>

```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/bloodhound/vid.gif?raw=true "Obtener datos del AD")


```
# Ejecutar bloodhound y cargar datos

# Ejecutar neo4j en una terminal
sudo neo4j console
# Ejecutar bloodhound en otra terminal
bloodhound
```
![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/bloodhound/vid2.gif?raw=true "Cargar datos en bloodhound")


```
# Consultas Bloodhound

# Show all domains and computer
MATCH p = (d:Domain)-[r:Contains*1..]->(n:Computer) RETURN p
# Show all the users
MATCH p = (d:Domain)-[r:Contains*1..]->(n:User) RETURN p
# Overall map of domains/groups/users
MATCH q=(d:Domain)-[r:Contains*1..]->(n:Group)<-[s:MemberOf]-(u:User) RETURN q
# See the users ACL
MATCH p=(u:User)-[r1]->(n) WHERE r1.isacl=true and not tolower(u.name) contains 'vagrant' RETURN p
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/bloodhound/vid3.gif?raw=true "Cargar datos en bloodhound")
