# Crear o Eliminar usuarios del dominio

```Bash
# Obtener una shell remota de un equipo con permisos de administracion del dominio
impacket-wmiexec <Dominio>/<Admin user>:'<Admin pass>'@<IP target>
# Eliminar usuario de dominio en la shell remota
net user <user> /DELETE /DOMAIN
# Añadir usuario de dominio en la shell remota
net user <user> <pass> /ADD /DOMAIN
# Añadir usuario de dominio al grupo del dominio deseado
net localgroup <nombre del grupo> <user> /add
```

# Crear o Elimindar usuario local

```Bash
# Obtener una shell remota de un equipo con permisos de administracion del dominio
impacket-wmiexec <Dominio>/<Admin user>:'<Admin pass>'@<IP target>
# Eliminar usuario local en la shell remota
net user /add <user> <pass>
# Añadir usuario local en la shell remota
net user /delete <user> <pass>
```

# Cambiar contraseña
```Bash
net user <user> newpassword
```

