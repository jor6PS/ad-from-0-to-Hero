# Obtenicion solo de usuarios

```Bash
# Obtener todos los usuarios con impaket
GetADUsers.py -all <nombre dominio completo>/<usuario>:<contraseña> > users.txt

```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_domain_info/files/users.gif?raw=true "Obteniendo todos los usuarios del dominio")

# Obtenicion toda la informacion de suarios

```Bash
# Obtener toda la información de los usuarios
ldapsearch -H ldap://<DC IP> -D "<user>@<domain>" -w <pass> -b 'DC=<domain>,DC=<extension>' "(&(objectCategory=person)(objectClass=user))" > users_full.txt
# Después usar grp para identificar posibles credenciales en la descripcion
cat users_full.txt| grep -E 'name|description'

```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_domain_info/files/users.png?raw=true "Obteniendo toda la info")


# Otros comandos útiles

```Bash
# List all users
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(&(objectCategory=person)(objectClass=user))" | grep 'distinguishedName:'
# List of all kerberoastables users
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(&(objectClass=user)(servicePrincipalName=*)(!(cn=krbtgt))(!(userAccountControl:1.2.840.113556.1.4.803:=2)))" | grep 'distinguishedName:'
# List of all asrep-roastables users
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(&(objectClass=user)(userAccountControl:1.2.840.113556.1.4.803:=4194304))" | grep 'distinguishedName:'
# Find all Users that need to change password on next login.
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(&(objectCategory=user)(pwdLastSet=0))" | grep 'distinguishedName:'
# Find all Users that are almost Locked-Out
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(&(objectCategory=user)(badPwdCount>=4))" | grep 'distinguishedName:'
#Find all Users with *pass* or *pwd* in their description
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(&(objectCategory=user)(|(description=*pass*)(description=*pwd*)(description=*password*)(description=*contraseña*)))" | grep 'distinguishedName:'
# List of all users protected by adminCount
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(&(objectCategory=user)(adminCount=1))" | grep 'distinguishedName:'
#List all groups
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(objectCategory=group)" | grep 'distinguishedName:'
# List of all groups protected by adminCount
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(&(objectCategory=group)(adminCount=1))" | grep 'distinguishedName:'
#Listing all servicePrincipalName
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(servicePrincipalName=*)" | grep 'distinguishedName:'
#Listing specific services from their servicePrincipalName
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(servicePrincipalName=http/*)" | grep 'distinguishedName:'
#Listing all computers with a given Operating System
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(&(objectCategory=Computer)(operatingSystem=Windows XP*))" | grep 'distinguishedName:'
# Find all Workstations
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(sAMAccountType=805306369)" | grep 'distinguishedName:'
# Find all computers having a KeyCredentialLink
ldapsearch -H ldap://<ldap ip> -D "<user>@<nombre dominio completo>" -w <pass> -b 'DC=<subdomain>,DC=<domain>,DC=<domain extension>' "(&(objectClass=computer)(msDS-KeyCredentialLink=*))" | grep 'distinguishedName:'

```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/valid_credentials/get_domain_info/files/vid.gif?raw=true "Obteniendo info del dominio")
