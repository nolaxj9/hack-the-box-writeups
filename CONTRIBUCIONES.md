# 🤝 Guía de Contribuciones

¡Gracias por tu interés en contribuir a este proyecto! Este documento explica cómo hacerlo de forma profesional.

---

## 📋 Tipos de Contribuciones

### 1. 📝 Nuevos Writeups de Máquinas

**¿Qué es?** Documentación completa de una máquina HTB completada.

**Pasos:**
```bash
# 1. Fork el repositorio (en GitHub)
# 2. Clona tu fork
git clone https://github.com/TU_USUARIO/hack-the-box-writeups.git
cd hack-the-box-writeups

# 3. Crea una rama para tu máquina
git checkout -b feat/maquina-nombre
# Ejemplo: git checkout -b feat/maquina-retired

# 4. Copia la plantilla
cp Tools/HTB_Documentation_Template.md Machines/Easy/Mi_Maquina.md
# (Ajusta la carpeta según dificultad: Easy, Medium, Hard)

# 5. Completa el writeup
vim Machines/Easy/Mi_Maquina.md

# 6. Verifica que incluyas:
# ✅ Las 4 fases PETS (Reconocimiento, Enumeración, Explotación, Post-Explotación)
# ✅ Tácticas MITRE ATT&CK
# ✅ Herramientas y comandos específicos
# ✅ Lecciones aprendidas
# ✅ Referencias y recursos

# 7. Haz commit
git add Machines/Easy/Mi_Maquina.md
git commit -m "✅ Writeup: Mi_Maquina [Easy] - Explotación de XSS"

# 8. Push a tu fork
git push origin feat/maquina-nombre

# 9. Abre un Pull Request en GitHub
# (GitHub te mostrará un botón "Compare & pull request")
```

**Checklist de Calidad:**
- [ ] Incluye todas las 4 fases PETS
- [ ] Mapea tácticas MITRE ATT&CK
- [ ] Comandos tienen explicaciones
- [ ] Evidencia visual (screenshots/outputs)
- [ ] Lecciones aprendidas documentadas
- [ ] Ortografía y gramática correctas
- [ ] Sin información sensible (credenciales reales)

---

### 2. 🐛 Reportar Errores

**¿Qué es?** Encontraste un error, comando incorrecto o información desactualizada.

**Pasos:**
```bash
# 1. Ve a GitHub → Issues
# 2. Click en "New Issue"
# 3. Elige "Bug report"
```

**Formato:**
```markdown
## 🐛 Descripción del Error
[Descripción clara del problema]

## 📍 Ubicación
- Archivo: `Machines/Easy/Lame.md`
- Línea: 45
- Sección: "Fase 2: Enumeración"

## 🔍 Comando Problemático
```bash
nmap -p- -sV 10.10.11.x  # Este comando no genera output esperado
```

## ✅ Solución Sugerida
```bash
nmap -p- -sV -sC 10.10.11.x
```

## 🖼️ Evidencia
[Adjunta screenshot si es posible]
```

---

### 3. 💡 Sugerencias y Mejoras

**¿Qué es?** Ideas para mejorar estructura, agregar contenido o optimizar.

**Pasos:**
```bash
# 1. GitHub → Issues → New Issue
# 2. Elige "Feature request"
```

**Formato:**
```markdown
## 💡 Sugerencia: [Título Descriptivo]

## 🎯 Descripción
[Explica qué quieres que se agregue]

## ✨ Beneficio
[Por qué sería útil]

## 📚 Recursos Relacionados
- [Link 1]
- [Link 2]

## 🎨 Ejemplo o Prototipo
[Si aplica, muestra cómo se vería]
```

---

### 4. 🔧 Mejoras de Herramientas

**¿Qué es?** Mejoras a plantillas, scripts o guías existentes.

**Ejemplos:**
- Agregar validación a `HTB_Interactive_Template.html`
- Mejorar `linpeas.sh` output parsing
- Actualizar `HTB_Quick_Commands.md` con nuevos comandos
- Agregar nuevas técnicas a `PETS_Framework_Guide.md`

**Pasos:**
```bash
# 1. Crea rama
git checkout -b improve/descripcion-mejora
# Ejemplo: git checkout -b improve/agregar-validacion-html

# 2. Modifica el archivo
vim Tools/HTB_Interactive_Template.html

# 3. Testea (si es código)
# 4. Commit
git commit -m "🔧 Mejora: Agregar validación a formulario HTML"

# 5. Push y Pull Request
git push origin improve/descripcion-mejora
```

---

### 5. 📚 Agregar Recursos Educativos

**¿Qué es?** Nuevas guías, tutoriales o referencias.

**Dónde van:**
- Conceptos técnicos: `Resources/Conceptos/`
- Scripts útiles: `Resources/Scripts/`
- Wordlists: `Resources/Wordlists/`
- Documentación: `Documentation/`

**Pasos:**
```bash
git checkout -b docs/tema-nuevo
# Ejemplo: git checkout -b docs/xss-avanzado

vim Resources/Conceptos/XSS_Avanzado.md
git add Resources/Conceptos/XSS_Avanzado.md
git commit -m "📚 Documento: XSS Avanzado - Técnicas y Mitigaciones"
git push origin docs/tema-nuevo
```

---

## 🎯 Estándares de Código y Estilo

### Markdown
```markdown
# Encabezado nivel 1
## Encabezado nivel 2
### Encabezado nivel 3

**Negrita** para énfasis
*Itálica* para ejemplos
`código inline` para comandos cortos

\`\`\`bash
# Bloques de código con sintaxis highlighting
echo "Hola mundo"
\`\`\`

- Listas
- Con puntos
  - Y subniveles

1. Listas
2. Numeradas
   1. Con subniveles

| Tabla | Profesional |
|-------|-------------|
| Usa | Tablas |
```

### Emojis Estándar
```
🎯 Objetivo/Meta
✅ Completo/Éxito
❌ Error/Fallo
⚠️ Advertencia
🔍 Búsqueda/Análisis
📡 Escaneo/Enumeración
💥 Explotación/Ataque
🚀 Escalada/Acceso
📚 Aprendizaje/Documentación
🔧 Herramientas/Mejora
🐛 Bug/Problema
💡 Idea/Sugerencia
📝 Documentación
🔐 Seguridad
🚩 Flag/Objetivo alcanzado
```

### Convención de Commits
```bash
# Formato: <tipo>(<scope>): <asunto>

git commit -m "✅ feat(writeup): Agregar máquina Lame [Easy]"
git commit -m "🐛 fix(commands): Corregir sintaxis comando nmap"
git commit -m "📚 docs(guide): Mejorar explicación PETS fase 1"
git commit -m "🔧 refactor(template): Reorganizar secciones markdown"

# Tipos:
# feat     - Nueva funcionalidad/writeup
# fix      - Corrección de error
# docs     - Cambios en documentación
# refactor - Cambios sin funcionalidad nueva
# style    - Formato/estilo
# test     - Tests
# chore    - Tareas de mantenimiento
```

---

## 📋 Antes de Hacer Push

### Checklist General
- [ ] Mi código/contenido sigue los estándares del proyecto
- [ ] Probé mi contribución (si aplica)
- [ ] Sin información sensible (credenciales, IPs reales, etc.)
- [ ] Incluyo referencias y fuentes
- [ ] Mi commit message es descriptivo
- [ ] Mi rama está actualizada con `main`

### Antes de Pull Request
```bash
# 1. Actualiza tu rama
git fetch origin
git rebase origin/main

# 2. Si hay conflictos, resuélvelos
# 3. Verifica cambios
git diff origin/main

# 4. Push
git push origin tu-rama

# 5. En GitHub, abre Pull Request
```

### Template de Pull Request

```markdown
## 📝 Descripción
[Describe qué agregaste/mejoraste]

## 🎯 Tipo de Cambio
- [ ] 📝 Nuevo writeup
- [ ] 🐛 Bug fix
- [ ] ✨ Nueva funcionalidad
- [ ] 📚 Documentación
- [ ] 🔧 Mejora

## 🔍 Cambios Realizados
- [Cambio 1]
- [Cambio 2]

## ✅ Checklist
- [ ] Mi código sigue los estándares
- [ ] Probé los cambios
- [ ] Sin información sensible
- [ ] Actualizé documentación si necesario

## 📚 Relacionado con
Cierra #XXX (número del issue si aplica)
```

---

## 🚀 Guía Rápida para Primeros Pasos

**Si es tu primer Pull Request:**

```bash
# 1. Crea una cuenta GitHub (si no tienes)
# 2. Haz fork del repositorio
# 3. Clona tu fork
git clone https://github.com/TU_USUARIO/hack-the-box-writeups.git
cd hack-the-box-writeups

# 4. Configura upstream
git remote add upstream https://github.com/USUARIO_ORIGINAL/hack-the-box-writeups.git

# 5. Crea rama
git checkout -b mi-primera-contribucion

# 6. Haz cambios
# 7. Commit
git commit -m "✨ feat: Mi primera contribución"

# 8. Push a tu fork
git push origin mi-primera-contribucion

# 9. En GitHub, haz click en "Compare & pull request"

# Después que aprueben:
git checkout main
git pull upstream main
git branch -d mi-primera-contribucion
```

---

## 📞 Soporte y Preguntas

¿Tienes preguntas?

1. **Lee la documentación** primero
2. **Busca en Issues** si alguien ya preguntó
3. **Abre una Discussion** (si está habilitada)
4. **Abre un Issue** con la etiqueta `question`

---

## 🎓 Recursos Útiles

- [Guía GitHub - Forking](https://guides.github.com/activities/forking/)
- [Guía Git - Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
- [Convencionalcommits.org](https://www.conventionalcommits.org/)

---

## 🙏 Agradecimientos

Gracias a todos los que contribuyen. ¡Tu esfuerzo ayuda a otros a aprender pentesting!

---

<div align="center">

**¡Esperamos tu contribución! 🚀**

⭐ Si encontraste útil este proyecto, dale una estrella ⭐

</div>
