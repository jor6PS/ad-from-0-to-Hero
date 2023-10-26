# **Table of Contents**
  
- **RECONOCIMIENTO**
  - *Sin credenciales*
    - [Escaneo de red](no_credentials/scan_network/): Nmap | Crackmapexec | ICMP-SCAN
    - [Listado de accesos sin credenciales y carpetas compartidas](no_credentials/list_guest_access_on_smb_share/): _Enum4linux-ng | Crackmapexec_
    - [Listar usuarios](no_credentials/find_user_list/): _Enum4linux | net rpc | Crackmapexec_
    - [Localizar ip de DC](no_credentials/find_dc_ip/): _NSLookup_
    - [Enumerar ldap](no_credentials/enumerate_ldap/): _Nmap_
  - *Con usuario, sin contraseña*
    - [ASEREPRoast](user_but_no_credentials/ASREPRoast/): _GetNPUsers.py impaket | Crackmapexec_
    - [Password spray](user_but_no_credentials/password_spray/): _Sprayhound | Crackmapexec_
    - [Crackeo de contraseñas](user_but_no_credentials/crack_passwords/): _Name-thath-hash | Hashcat_
  - *Credenciales válidas*
    - [Política de contraseñas](valid_credentials/pass_pol/): _Crackmapexec_
    - [Obtener todos los usuarios](valid_credentials/get_all_users/): _GetADUsers.py impaket_
    - [kerberoasting](valid_credentials/kerberoasting/): _GetUsersSPN.py impaket crackmpexec | name-that-hash hashcat_
    - [Comandos útiles para recoger info del dominio](valid_credentials/useful_domain_info/): _ldapsearch_
    - [Get DNS IP](valid_credentials/get_dns/): _Adidnsdump_
    - [Bloodhound get AD info](valid_credentials/bloodhound/): _Bloodhound_
