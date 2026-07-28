# 🎯 Hack the Box - Metodología PETS + MITRE ATT&CK

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Linux](https://img.shields.io/badge/Linux-red.svg)](https://www.linux.org/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black.svg)](https://github.com/)

Documentación exhaustiva y profesional de máquinas de [Hack the Box](https://www.hackthebox.com/) siguiendo la metodología **PETS** (Passive, Enumeration, Tracking, Scanning) integrada con el framework **MITRE ATT&CK**.

Este repositorio es tanto un **portafolio de pentesting** como una **guía práctica** para aprender seguridad ofensiva de forma profesional.

---

## 📚 Contenido del Repositorio

```
hack-the-box-writeups/
├── 📋 README.md                           # Este archivo
├── 📝 CONTRIBUCIONES.md                   # Cómo contribuir
├── 📊 ROADMAP.md                          # Planes futuros
│
├── 🎯 Machines/                           # Documentación de máquinas
│   ├── Easy/
│   │   ├── Lame.md                        # Writeup completo
│   │   ├── Legacy.md
│   │   └── Blue.md
│   ├── Medium/
│   │   ├── Kioptrix.md
│   │   └── Shocker.md
│   └── Hard/
│       ├── Pwn3d.md
│       └── HacktheBox-1.md
│
├── 🛠️ Tools/                              # Herramientas y recursos
│   ├── HTB_Documentation_Template.md      # Plantilla para documentar
│   ├── HTB_Interactive_Template.html      # Herramienta interactiva
│   ├── HTB_Quick_Commands.md              # Referencia de comandos
│   ├── PETS_Framework_Guide.md            # Explicación PETS
│   └── MITRE_ATT&CK_Reference.md         # Referencia ATT&CK
│
├── 📚 Resources/                          # Recursos educativos
│   ├── Conceptos/
│   │   ├── SQL_Injection.md
│   │   ├── RCE_and_Shells.md
│   │   ├── Privilege_Escalation.md
│   │   └── Persistence.md
│   ├── Scripts/
│   │   ├── linpeas.sh
│   │   ├── privesc_exploits/
│   │   └── reverse_shells/
│   └── Wordlists/
│       ├── common.txt
│       └── dirnames.txt
│
├── 📖 Documentation/                      # Documentación adicional
│   ├── Setup_Guide.md                     # Guía de instalación
│   ├── Methodology.md                     # Metodología completa
│   └── Best_Practices.md                  # Mejores prácticas
│
└── .gitignore                             # Archivo de exclusiones

```

---

## 🚀 Inicio Rápido

### Requisitos Previos
- Kali Linux o distribución similar
- Python 3.8+
- Herramientas básicas: `nmap`, `curl`, `git`
- Cuenta en [Hack the Box](https://www.hackthebox.com/)

### Instalación

```bash
# Clonar el repositorio
git clone https://github.com/TU_USUARIO/hack-the-box-writeups.git
cd hack-the-box-writeups

# (Opcional) Crear ambiente virtual
python3 -m venv venv
source venv/bin/activate

# Instalar dependencias
pip install -r requirements.txt
```

### Uso

**1. Para estudiar una máquina:**
```bash
# Abre la documentación de la máquina
cat Machines/Easy/Lame.md

# O usa la plantilla interactiva
firefox Tools/HTB_Interactive_Template.html
```

**2. Para documentar tu propia máquina:**
```bash
# Copia la plantilla
cp Tools/HTB_Documentation_Template.md Machines/Easy/Mi_Maquina.md

# Edita con tu editor favorito
vim Machines/Easy/Mi_Maquina.md

# Haz commit cuando termines
git add Machines/Easy/Mi_Maquina.md
git commit -m "✅ Máquina completada: Mi_Maquina [Easy]"
git push
```

**3. Para buscar comandos:**
```bash
# Usa la guía rápida
grep -i "reverse shell" Tools/HTB_Quick_Commands.md

# O visualiza todo
less Tools/HTB_Quick_Commands.md
```

---

## 📖 Metodología PETS + MITRE ATT&CK

### PETS (4 Fases del Pentesting)

```
1️⃣ PASSIVE RECON        →  Información sin contacto directo
   - WHOIS, DNS, Shodan, Google Dorks
   - Tácticas MITRE: Reconnaissance

2️⃣ ENUMERATION           →  Escaneo y análisis detallado
   - Nmap, Gobuster, SQLmap, Nikto
   - Tácticas MITRE: Discovery, Initial Access

3️⃣ EXPLOITATION          →  Ataque y obtención de acceso
   - Metasploit, RCE, SQL Injection, Shells
   - Tácticas MITRE: Execution, Initial Access

4️⃣ POST-EXPLOITATION     →  Escalada y consolidación
   - Privilege Escalation, Persistence
   - Tácticas MITRE: Privilege Escalation, Defense Evasion
```

### Integración con MITRE ATT&CK

Cada writeup documenta las **tácticas y técnicas** usadas según el framework [MITRE ATT&CK](https://attack.mitre.org/), mapeando ataques del mundo real con la terminología profesional.

**Ejemplo:**
```markdown
## Fase 3: Explotación

**Vulnerabilidad:** SQL Injection en login.php
**Técnica MITRE ATT&CK:** T1190 - Exploit Public-Facing Application
**CVE:** CVE-2021-XXXXX
**Comando:** sqlmap -u "http://target.com/login.php" --dbs
```

---

## 📊 Estadísticas y Progreso

| Nivel | Completadas | En Progreso | Planeadas |
|-------|------------|-------------|----------|
| 🟩 **Easy** | 3 | 2 | 10 |
| 🟨 **Medium** | 1 | 1 | 15 |
| 🟥 **Hard** | 0 | 0 | 5 |
| **TOTAL** | **4** | **3** | **30** |

*Última actualización: [Fecha]*

---

## 🎓 Lo Que Aprendí

### Conceptos Clave
- ✅ Reconocimiento pasivo y activo
- ✅ SQL Injection y explotación web
- ✅ Shells inversos y RCE
- ✅ Escalada de privilegios en Linux/Windows
- ✅ Análisis de vulnerabilidades con Nmap
- ✅ Metasploit Framework
- ✅ Enumeración SMB y LDAP
- ✅ Cracking de contraseñas (John, Hashcat)

### Herramientas Dominadas
- 🔧 **Nmap** - Escaneo de puertos y servicios
- 🔧 **Metasploit** - Framework de explotación
- 🔧 **Burp Suite** - Análisis web
- 🔧 **SQLmap** - SQL Injection automatizado
- 🔧 **John the Ripper** - Cracking de contraseñas
- 🔧 **Mimikatz** - Extracción de credenciales

---

## 🛠️ Plantillas y Herramientas Incluidas

### 📋 Plantillas

1. **HTB_Documentation_Template.md**
   - Plantilla Markdown completa
   - Secciones para cada fase PETS
   - Integración MITRE ATT&CK
   - Espacio para lecciones aprendidas

2. **HTB_Interactive_Template.html**
   - Herramienta web interactiva
   - Formulario visual
   - Exportación automática a Markdown
   - Previsualización en tiempo real

### 📚 Guías de Referencia

- **HTB_Quick_Commands.md** - Comandos por fase (200+ líneas)
- **PETS_Framework_Guide.md** - Explicación detallada de PETS
- **MITRE_ATT&CK_Reference.md** - Mapeo de tácticas

### 🎯 Scripts

- **linpeas.sh** - Enumeración automática Linux
- **privesc_exploits/** - Exploits de escalada
- **reverse_shells/** - Colección de shells inversos

---

## 📝 Estructura de un Writeup

Cada máquina documentada sigue esta estructura:

```markdown
# Nombre de la Máquina

## Información General
- Dificultad: 🟩 Fácil
- IP: 10.10.11.XXX
- SO: Linux

## 🔍 Fase 1: Reconocimiento Pasivo
- Información WHOIS
- Datos de Shodan
- Búsquedas previas

## 📡 Fase 2: Enumeración
- Resultados Nmap
- Puertos abiertos
- Servicios y versiones
- Vulnerabilidades identificadas

## 💥 Fase 3: Explotación
- Método elegido
- Comandos ejecutados
- Acceso obtenido

## 🚀 Fase 4: Post-Explotación
- Escalada de privilegios
- Flags capturadas
- Limpiar huellas

## 📚 Lecciones Aprendidas
- Conceptos clave
- Herramientas útiles
- Lo que haría diferente
```

---

## 🤝 Contribuciones

¡Las contribuciones son bienvenidas! Puedes:

- 📝 Agregar nuevos writeups
- 🐛 Reportar errores o mejoras
- 💡 Sugerir nuevas máquinas
- 🔧 Mejorar herramientas existentes
- 📚 Agregar recursos educativos

Ver [CONTRIBUCIONES.md](CONTRIBUCIONES.md) para detalles.

---

## 📚 Recursos Externos

### Plataformas de Práctica
- [Hack the Box](https://www.hackthebox.com/) - Plataforma principal
- [TryHackMe](https://tryhackme.com/) - Máquinas guiadas
- [PentesterLab](https://pentesterlab.com/) - Ejercicios web
- [HackTheBoxEasy](https://app.hackthebox.com/machines?tab=my_machines) - Máquinas Easy

### Documentación Oficial
- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [Exploit-DB](https://www.exploit-db.com/)
- [HackTricks](https://book.hacktricks.xyz/)

### Canales de Aprendizaje
- [IppSec en YouTube](https://www.youtube.com/c/IppSec) - Walkthroughs HTB
- [NetworkChuck en YouTube](https://www.youtube.com/c/NetworkChuck)
- [SANS Cyber Aces](https://www.cybrary.it/)

---

## 📋 Checklist de Mejora

- [ ] Agregar 5 máquinas Easy
- [ ] Agregar 3 máquinas Medium
- [ ] Scripts de automación completos
- [ ] Guía de configuración de lab local
- [ ] CI/CD para validar documentación
- [ ] Sistema de tags por técnica
- [ ] Videos explicativos
- [ ] Bot para actualizar estadísticas automáticamente

Ver [ROADMAP.md](ROADMAP.md) para el plan completo.

---

## ⚖️ Licencia

Este proyecto está bajo la licencia **MIT**. Puedes usarlo, modificarlo y distribuirlo libremente.

Ver [LICENSE](LICENSE) para detalles completos.

---

## 📧 Contacto y Redes

- **GitHub:** [@tu_usuario](https://github.com/tu_usuario)
- **LinkedIn:** [Tu Perfil](https://linkedin.com/in/tu_usuario)
- **Twitter:** [@tu_usuario](https://twitter.com/tu_usuario)
- **Email:** tu.email@example.com

---

## ⭐ Apoyo

Si encontraste útil este repositorio:

1. ⭐ **Dale una estrella** (star) en GitHub
2. 📤 **Comparte** con otros estudiantes de seguridad
3. 🔔 **Sígueme** para nuevas actualizaciones
4. 💬 **Abre issues** con sugerencias

---

## 📄 Notas Importantes

⚠️ **Disclaimer Legal:**
- Este repositorio es **solo para fines educativos**
- Solo ataca sistemas en los que tienes **autorización explícita**
- Usa siempre **responsablemente** tus conocimientos de seguridad
- El autor no es responsable de uso indebido de esta información

---

<div align="center">

### 🎯 Hecho con ❤️ por alguien aprendiendo Pentesting

![Hack the Box Badge](https://www.hackthebox.com/badge/image/YOUR_ID)

**Última actualización:** 2024  
**Versión:** 1.0.0  
**Estado:** 🟢 Activo

</div>
