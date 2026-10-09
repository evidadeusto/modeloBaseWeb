🌐 **ELIGE TU IDIOMA / CHOOSE YOUR LANGUAGE**

🇪🇸 **[ESPAÑOL](#-modelobaseweb-es)** | 🇬🇧 **[ENGLISH](#-modelobaseweb-en)**

---

# 🌐 modeloBaseWeb (ES)

### Plantilla Profesional de Sitio Web con Django + Docker

> **Un punto de partida sólido para construir aplicaciones web modernas, escalables y profesionales. Con dos caminos: aprende desde cero o usa el template listo.**

[![Django](https://img.shields.io/badge/Django-4.2+-092E20?style=for-the-badge&logo=django&logoColor=white)](https://www.djangoproject.com/)
[![Docker](https://img.shields.io/badge/Docker-Latest-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

## ¿Qué es modeloBaseWeb?

`modeloBaseWeb` es una **plantilla profesional y escalable** para crear sitios web funcionales usando **Django** (framework Python) y **Docker** (contenedores). 

**Perfecto para:**
- ✅ Aprender la arquitectura profesional de Django desde cero
- ✅ Usar un template listo para producción
- ✅ Equipos que necesitan estandarizar proyectos
- ✅ Aplicaciones que requieren Docker desde el inicio

---

## DOS CAMINOS - Elige el tuyo

### Ruta 1: **APRENDER DESDE CERO** 
**Para desarrolladores que quieren entender la arquitectura**

```
    RAMA/BRANCH: main
📄  ARCHIVO: GUIA.MD
⏱️  TIEMPO: 2-3 horas (completo)
📚  NIVEL: Principiante → Intermedio
```

**¿Qué incluye?**
- 3 fases completas paso a paso
- Explicación de cada comando
- Estructura profesional desde cero
- Buenas prácticas de Docker

**¿Para quién?**
- Quiero entender cómo funciona Django + Docker
- Necesito aprender la arquitectura
- Prefiero construir desde los fundamentos

 > [!NOTE] 
 > Si eliges APRENDER DESDE CERO **👉 [Abre GUIA.MD →](./GUIA.MD)**; sigue los 3 pasos (FASE 1, 2, 3), aprende cada concepto y construye tu primer sitio web

---

### Ruta 2: **USAR TEMPLATE LISTO**
**Para desarrolladores que necesitan un proyecto funcional al instante**

| Idioma | Rama | Comando |
|--------|------|---------|
| **Español** | `template-es` | `git clone --branch template-es <repo-url>` |
| **Inglés** | `template-en` | `git clone --branch template-en <repo-url>` |

**¿Qué incluye?**
- Proyecto completamente configurado
- Docker Compose profesional
- Base de datos lista
- Panel admin funcional
- Todo listo para customizar

**¿Para quién?**
- Necesito un proyecto funcional en 5 minutos
- Ya conozco Django y Docker

---

## 📊 Comparativa: Aprender vs Template

| Aspecto | 🎓 Aprender | 🚀 Template |
|---------|-----------|-----------|
| **Tiempo setup** | 2-3 horas | 5 minutos |
| **¿Entiendas la arquitectura?** | ✅ SÍ (completo) | ⚠️ Básicamente |
| **¿Proyecto funcional?** | ✅ SÍ (al final) | ✅ SÍ (inmediato) |
| **Ideal para...** | Aprender | Producción |
| **Dificultad** | Paso a paso | Plug & play |
| **Customización** | Desde cero | Modifica según necesites |
| **Rama** | `main` | `template-es` / `template-en` |

---
## Requisitos Previos

Ambas rutas necesitan:

- **Docker Desktop** — [Descargar](https://www.docker.com/products/docker-desktop)
- **Visual Studio Code** — [Descargar](https://code.visualstudio.com/download)
- **Git** — [Descargar](https://git-scm.com/)

---

## 📁 Estructura de Ramas

```
main (ESTÁS AQUÍ)
├─ 📄 README.md (este archivo)
├─ 📚 GUIA.MD (tutorial completo)
│
└─ Ramas:
    ├─ template-es (Django + Docker listos en ESPAÑOL)
    └─ template-en (Django + Docker listos en INGLÉS)
```
---


## FAQ - Preguntas Frecuentes ❓ 

**P: ¿Necesito experiencia previa con Django o Docker?**
> R: No, la GUÍA te enseña desde cero. Ambas rutas están pensadas para principiantes.

**P: ¿Qué diferencia hay entre las ramas?**
> R: La rama `main` tiene la guía de aprendizaje. Las ramas `template-es` y `template-en` son proyectos completamente funcionales listos para usar.

**P: ¿Puedo usar esto en producción?**
> R: Sí, Docker Compose está configurado profesionalmente. Las ramas template incluyen mejores prácticas.

**P: ¿Qué idioma tiene cada rama?**
> R: `template-es` → Español | `template-en` → Inglés. La guía GUIA.MD está en español.

**P: ¿Dónde veo mi sitio web?**
> R: En `http://localhost:3000`

**P: ¿Cómo accedo al panel de admin?**
> R: `http://localhost:3000/admin` (con credenciales del superusuario que creaste)

**P: ¿Puedo cambiar de Django a otro framework?**
> R: Este template está optimizado para Django, pero la estructura Docker es reutilizable.

**P: ¿Cómo agrego nuevas páginas?**
> R: En la GUÍA (FASE 2) aprenderás a crear apps y templates. En template: copia la estructura existente.

**P: ¿Docker consume muchos recursos?**
> R: No, Docker es eficiente. Las imágenes python:3.11-slim son pequeñas (~150MB).

---

## 📚 ¿Por dónde empiezo?

### Si ERES PRINCIPIANTE:
```
1. Verifica tener Docker instalado → docker --version
2. Abre GUIA.MD en esta rama
3. Sigue paso a paso
4. Aprende la arquitectura completa
```

### Si TIENES EXPERIENCIA:
```
1. Haz fork de template-es o template-en
2. docker-compose up
3. Personaliza según necesites
4. Deploy a producción
```

---

## 🤝 Contribuciones

¿Tienes mejoras o sugerencias?

- 🐛 **Reportar bugs** — [Issues](https://github.com/evidadeusto/modeloBaseWeb/issues)
- 🔀 **Hacer pull requests** — Tus contribuciones son bienvenidas

---

## 📄 Licencia

Este proyecto se distribuye bajo la licencia **MIT**. Eres libre de usar, modificar y distribuir el código.


---

## 💬 Conecta Conmigo

**¿Preguntas o sugerencias?**

💼 **LinkedIn:** [Juliam Guerrero Diaz](https://www.linkedin.com/in/juliamguerrero/)  
📧 **Email:** [juliamdario.g@deusto.es](mailto:juliamdario.g@deusto.es)  
🐙 **GitHub:** [@JULIAMGUERRERO](https://github.com/JULIAMGUERRERO)

---

⭐ **Si este proyecto te es útil, ayuda a otros dejando una estrella en GitHub** ⭐

---

# 🌐 modeloBaseWeb (EN)

### Professional Website Template with Django + Docker

> **A solid starting point for building modern, scalable, and professional web applications. With two paths: learn from scratch or use the ready-made template.**

[![Django](https://img.shields.io/badge/Django-4.2+-092E20?style=for-the-badge&logo=django&logoColor=white)](https://www.djangoproject.com/)
[![Docker](https://img.shields.io/badge/Docker-Latest-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

## What is modeloBaseWeb?

`modeloBaseWeb` is a **professional and scalable template** for creating functional websites using **Django** (Python framework) and **Docker** (containers).

**Perfect for:**
- ✅ Learning Django's professional architecture from scratch
- ✅ Using a production-ready template
- ✅ Teams that need to standardize projects
- ✅ Applications that require Docker from the start

---

## TWO PATHS - Choose yours

### Path 1: **LEARN FROM SCRATCH** 
**For developers who want to understand the architecture**

```
    BRANCH: main
📄  FILE: GUIA.MD
⏱️  TIME: 2-3 hours (complete)
📚  LEVEL: Beginner → Intermediate
```

**What does it include?**
- 3 complete phases step by step
- Explanation of each command
- Professional structure from scratch
- Docker best practices

**For whom?**
- I want to understand how Django + Docker works
- I need to learn the architecture
- I prefer to build from the foundations

 > [!NOTE] 
 > If you choose LEARN FROM SCRATCH **👉 [Open GUIDE.MD →](./GUIDE.MD)**; follow the 3 steps (PHASE 1, 2, 3), learn each concept and build your first website

---

### Path 2: **USE READY TEMPLATE**
**For developers who need a functional project instantly**

| Language | Branch | Command |
|----------|--------|---------|
| **Spanish** | `template-es` | `git clone --branch template-es <repo-url>` |
| **English** | `template-en` | `git clone --branch template-en <repo-url>` |

**What does it include?**
- Completely configured project
- Professional Docker Compose
- Database ready
- Functional admin panel
- Everything ready to customize

**For whom?**
- I need a functional project in 5 minutes
- I already know Django and Docker

---

## 📊 Comparison: Learn vs Template

| Aspect | 🎓 Learn | 🚀 Template |
|--------|---------|-----------|
| **Setup time** | 2-3 hours | 5 minutes |
| **Understand architecture?** | ✅ YES (complete) | ⚠️ Basically |
| **Functional project?** | ✅ YES (at the end) | ✅ YES (immediate) |
| **Ideal for...** | Learning | Production |
| **Difficulty** | Step by step | Plug & play |
| **Customization** | From scratch | Modify as needed |
| **Branch** | `main` | `template-es` / `template-en` |

---
## Prerequisites

Both paths need:

- **Docker Desktop** — [Download](https://www.docker.com/products/docker-desktop)
- **Visual Studio Code** — [Download](https://code.visualstudio.com/download)
- **Git** — [Download](https://git-scm.com/)

---

## 📁 Branch Structure

```
main (YOU ARE HERE)
├─ 📄 README.md (this file)
├─ 📚 GUIA.MD (tutorial completo en ESPAÑOL)
├─ 📚 GUIDE.MD (complete tutorial in ENGLISH)
│
└─ Branches:
    ├─ template-es (Django + Docker ready in SPANISH)
    └─ template-en (Django + Docker ready in ENGLISH)
```
---


## FAQ - Frequently Asked Questions ❓ 

**Q: Do I need previous experience with Django or Docker?**
> A: No, the GUIDE teaches you from scratch. Both paths are designed for beginners.

**Q: What's the difference between the branches?**
> A: The `main` branch has the learning guide. The `template-es` and `template-en` branches are completely functional projects ready to use.

**Q: Can I use this in production?**
> A: Yes, Docker Compose is configured professionally. The template branches include best practices.

**Q: What language does each branch have?**
> A: `template-es` → Spanish | `template-en` → English. The guide GUIA.MD is in Spanish, GUIDE.MD is in English.

**Q: Where can I see my website?**
> A: At `http://localhost:3000`

**Q: How do I access the admin panel?**
> A: `http://localhost:3000/admin` (with superuser credentials you created)

**Q: Can I switch from Django to another framework?**
> A: This template is optimized for Django, but the Docker structure is reusable.

**Q: How do I add new pages?**
> A: In the GUIDE (PHASE 2) you'll learn to create apps and templates. In template: copy the existing structure.

**Q: Does Docker consume many resources?**
> A: No, Docker is efficient. Python 3.11-slim images are small (~150MB).

---

## 📚 Where do I start?

### If YOU ARE A BEGINNER:
```
1. Verify Docker is installed → docker --version
2. Open GUIDE.MD in this branch
3. Follow step by step
4. Learn the complete architecture
```

### If YOU HAVE EXPERIENCE:
```
1. Fork template-es or template-en
2. docker-compose up
3. Customize as needed
4. Deploy to production
```

---

## 🤝 Contributions

Do you have improvements or suggestions?

- 🐛 **Report bugs** — [Issues](https://github.com/evidadeusto/modeloBaseWeb/issues)
- 🔀 **Make pull requests** — Your contributions are welcome

---

## 📄 License

This project is distributed under the **MIT** license. You are free to use, modify and distribute the code.

---

## 💬 Connect With Me

**Questions or suggestions?**

💼 **LinkedIn:** [Juliam Guerrero Diaz](https://www.linkedin.com/in/juliamguerrero/)  
📧 **Email:** [juliamdario.g@deusto.es](mailto:juliamdario.g@deusto.es)  
🐙 **GitHub:** [@JULIAMGUERRERO](https://github.com/JULIAMGUERRERO)

---

⭐ **If this project is useful to you, help others by leaving a star on GitHub** ⭐
