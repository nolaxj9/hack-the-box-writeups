# 🔧 Setup Guide - Configuración del Entorno

Guía completa para configurar tu entorno de trabajo para Hack the Box y pentesting.

---

## 📋 Requisitos Previos

### Sistema Operativo Recomendado
- **Kali Linux** (incluye la mayoría de herramientas)
- **Parrot OS** (alternativa)
- **Ubuntu/Debian** (requiere instalación manual)
- **macOS** (con homebrew)
- **Windows** (WSL2 recomendado)

### Recursos Mínimos
- RAM: 4GB (8GB recomendado)
- Disco: 20GB libre
- CPU: Dual-core mínimo

---

## 🐧 Instalación en Linux (Ubuntu/Debian)

### Paso 1: Actualizar Sistema

```bash
sudo apt update
sudo apt upgrade -y
```

### Paso 2: Instalar Herramientas Principales

```bash
sudo apt install -y \
  curl \
  wget \
  git \
  vim \
  python3 \
  python3-pip \
  build-essential \
  libssl-dev \
  libffi-dev \
  nmap \
  netcat-openbsd \
  socat \
  rlwrap \
  tmux \
  jq
```

### Paso 3: Instalar Herramientas de Pentesting

```bash
# Nikto (scanner web)
sudo apt install nikto

# Gobuster (descubrimiento de directorios)
sudo apt install gobuster

# SQLmap (SQL injection automatizado)
sudo apt install sqlmap

# John the Ripper (cracking)
sudo apt install john

# Hashcat (cracking avanzado)
sudo apt install hashcat

# Metasploit Framework
curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wf.erb > /tmp/metasploit-framework-wf.erb
sudo bash -c 'bash <(curl -sL https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/base-build.erb)'
```

### Paso 4: Instalar Python y Dependencias

```bash
# Actualizar pip
pip3 install --upgrade pip

# Instalar dependencias del proyecto
cd hack-the-box-writeups
pip3 install -r requirements.txt
```

### Paso 5: Verificar Instalación

```bash
# Verificar herramientas
nmap --version
gobuster --version
sqlmap --version
john --version
python3 --version
git --version

# Debería mostrar versiones sin errores
```

---

## 🍎 Instalación en macOS

### Paso 1: Instalar Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Paso 2: Instalar Herramientas

```bash
brew install \
  nmap \
  netcat \
  socat \
  wget \
  curl \
  git \
  python3 \
  tmux
```

### Paso 3: Herramientas desde Código Fuente

```bash
# Gobuster
brew install gobuster

# SQLmap
brew install sqlmap

# John
brew install john-jumbo

# Hashcat
brew install hashcat
```

### Paso 4: Metasploit (opcional)

```bash
# En macOS es más complicado
# Mejor usar Docker: docker run -it metasploitframework/metasploit-framework
```

---

## 🪟 Instalación en Windows

### Opción A: WSL2 (Recomendado)

```powershell
# Habilitar WSL2
wsl --install

# Descargar Ubuntu 22.04
# Microsoft Store → Ubuntu 22.04 LTS

# Una vez instalado, sigue guía de Linux anterior
```

### Opción B: Máquina Virtual

1. Descargar VirtualBox o VMware
2. Descargar ISO de Kali Linux
3. Crear VM con al menos 4GB RAM
4. Instalar como en Linux

---

## 🏠 Configuración de Carpetas

### Estructura Recomendada

```bash
~
├── HTB/                          # Carpeta principal
│   ├── writeups/                # Documentación
│   ├── machines/                # Datos de máquinas
│   ├── tools/                   # Scripts y exploits
│   ├── wordlists/               # Diccionarios
│   └── notes/                   # Apuntes personales
│
├── pentest-tools/               # Herramientas compiladas
│   ├── privesc/
│   ├── shells/
│   └── exploits/
│
└── VulnHub/                      # Máquinas locales (opcional)
```

### Crear Estructura

```bash
mkdir -p ~/HTB/{writeups,machines,tools,wordlists,notes}
mkdir -p ~/pentest-tools/{privesc,shells,exploits}
cd ~/HTB
git clone https://github.com/TU_USUARIO/hack-the-box-writeups.git
```

---

## 🌐 Configuración de Conectividad HTB

### Conectar a HTB VPN

#### 1. Descargar VPN

- Ve a Hack the Box
- Settings → VPN
- Descarga archivo `.ovpn`

#### 2. Conectar OpenVPN

```bash
# En Linux
sudo openvpn ~/tu_archivo.ovpn

# En macOS
brew install openvpn
sudo openvpn ~/tu_archivo.ovpn

# En Windows (WSL)
# O usar OpenVPN GUI
```

#### 3. Verificar Conexión

```bash
# Debería poder hacer ping a máquinas HTB
ping 10.10.11.x

# Si falla:
sudo systemctl restart networking
sudo openvpn ~/tu_archivo.ovpn &
```

---

## 🎯 Configuración de Bash/Shell

### Agregar Alias Útiles

```bash
# Editar ~/.bashrc o ~/.zshrc
vim ~/.bashrc

# Agregar al final:
alias htb='cd ~/HTB'
alias nmap-quick='nmap --top-ports 1000'
alias nmap-full='nmap -p- --open -sV -sC -A'
alias http-server='python3 -m http.server 8000'
alias web-server='php -S 0.0.0.0:8000'
alias nc-listen='rlwrap nc -lvnp'

# Recargar
source ~/.bashrc
```

### Configurar tmux

```bash
# Crear ~/.tmux.conf
cat > ~/.tmux.conf << 'EOF'
# Set prefix
set -g prefix C-b

# Enable mouse
set -g mouse on

# Colors
set -g default-terminal "screen-256color"

# Panes
bind v split-window -h
bind s split-window -v
EOF

# Recargar
tmux source ~/.tmux.conf
```

---

## 🔐 Configuración de SSH

### Generar SSH Key (para GitHub)

```bash
ssh-keygen -t ed25519 -C "tu.email@gmail.com"
# Presiona Enter cuando pregunte ubicación
# Presiona Enter cuando pregunte passphrase (o agrega una)

# Ver clave pública
cat ~/.ssh/id_ed25519.pub

# Agregar a GitHub:
# GitHub Settings → SSH and GPG keys → New SSH key
```

### Configurar SSH para HTB

```bash
# Crear ~/.ssh/config
cat > ~/.ssh/config << 'EOF'
# Hack the Box
Host htb
  HostName 10.10.11.x
  User username
  Port 22
  IdentityFile ~/.ssh/id_ed25519
EOF

# Ahora puedes: ssh htb
```

---

## 📚 Descargar Wordlists

```bash
# Rockyou (contraseñas comunes)
cd ~/HTB/wordlists
wget https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt

# Common usernames
wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Usernames/xato-net-10-million-usernames.txt

# Directorios web
wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common.txt

# Todos los diccionarios (300MB+)
git clone https://github.com/danielmiessler/SecLists.git
```

---

## 🐳 Docker Setup (Opcional)

### Instalar Docker

```bash
# Linux
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# macOS
brew install docker

# Windows
Descargar Docker Desktop desde docker.com
```

### Imagen de Pentesting

```bash
# Usar Kali Linux en Docker
docker run -it kalilinux/kali-linux-docker

# O crear Dockerfile personalizado:
# FROM ubuntu:22.04
# RUN apt update && apt install -y nmap nikto sqlmap
```

---

## ✅ Checklist Final

- [ ] Sistema operativo actualizado
- [ ] Herramientas principales instaladas
- [ ] VPN HTB funcionando
- [ ] Carpetas configuradas
- [ ] Alias de bash configurados
- [ ] SSH configurado
- [ ] Wordlists descargadas
- [ ] Python3 y pip funcionando
- [ ] Git configurado
- [ ] Puedo conectarme a máquinas HTB

---

## 🆘 Troubleshooting

### "Command not found: nmap"
```bash
# Instalar nmap
sudo apt install nmap

# O verificar PATH
which nmap
```

### "Permission denied: openvpn"
```bash
# OpenVPN requiere sudo
sudo openvpn ~/archivo.ovpn

# O agregar permisos
sudo usermod -aG dialout $USER
```

### "No connection to Hack the Box"
```bash
# Verificar VPN
ifconfig | grep tun

# Reiniciar VPN
sudo systemctl restart openvpn@client
```

### "Python3 not found"
```bash
# Instalar Python3
sudo apt install python3 python3-pip

# Verificar
python3 --version
```

---

## 📚 Recursos de Aprendizaje

### Documentación Oficial
- [Nmap Manual](https://nmap.org/book/)
- [SQLmap Wiki](https://github.com/sqlmapproject/sqlmap/wiki)
- [Metasploit Docs](https://docs.metasploit.com/)

### Cursos Online
- TryHackMe (gratuito)
- Hack the Box Academy
- SANS Cyber Aces

### Comunidades
- r/learnprogramming
- r/hacking
- Discord de HTB

---

<div align="center">

### ✅ Configuración Completa

**Ahora estás listo para el pentesting. ¡Buena suerte!**

</div>
