# Habilitar servicios para poder cargar o descargar información en otros sistemas de la red

```
# Usando smbserver de impaket
impacket-smbserver SHARE . -smb2support
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/utilities/Enable_servers_to_share_load_or_upload_content/smbshare.png?raw=true "smbserver")

```
# Usando modulo de python
python -m http.server
```

![Alt text](https://github.com/jor6PS/ad-from-0-to-Hero/blob/master/utilities/Enable_servers_to_share_load_or_upload_content/httpshare.png?raw=true "httpserver")
