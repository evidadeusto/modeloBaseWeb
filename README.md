# 🌐 modeloBaseWeb

### Plantilla Profesional de Sitio Web con Django + Docker

> **Un punto de partida sólido para construir aplicaciones web modernas, escalables y profesionales.**

[![Django](https://img.shields.io/badge/Django-4.2+-092E20?style=for-the-badge&logo=django&logoColor=white)](https://www.djangoproject.com/)
[![Docker](https://img.shields.io/badge/Docker-Latest-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

## ¿Qué es modeloBaseWeb?

`modeloBaseWeb` es una **plantilla profesional y escalable** para crear sitios web funcionales usando **Django** (framework Python) y **Docker** (contenedores). Incluye una estructura base completa, buenas prácticas de desarrollo y documentación paso a paso para llevarte desde cero hasta un proyecto web en producción.

**Perfecto para:**
- ✅ Desarrolladores que quieren un punto de partida profesional
- ✅ Equipos que necesitan estandarizar sus proyectos Django
- ✅ Aplicaciones web que requieren Docker desde el inicio
- ✅ Prototipado rápido con arquitectura escalable

---

## Soporte visual

### 🏠 Página de Inicio
![Homepage](/assets/imagesReadme/homepage.png)

### 📊 Panel de Administración
![Admin Panel](/assets/imagesReadme/admin-panel.png)

### 📱 Responsive Design
![Mobile View](/assets/imagesReadme/mobile-view.png)

---

## 🚀 Inicio Rápido (5 Pasos)

### Requisitos Previos
- **Docker Desktop** — [Descargar](https://www.docker.com/products/docker-desktop)
- **Visual Studio Code** — [Descargar](https://code.visualstudio.com/download)
- **Git** — [Descargar](https://git-scm.com/)

### Paso 1: Clonar el Repositorio

```bash
git clone https://github.com/JULIAMGUERRERO/modeloBaseWeb.git
cd modeloBaseWeb
```

### Paso A: Construir la Imagen Docker (Solo primera vez)

```bash
docker-compose build --no-cache
```

Esto crea la imagen con el tag `imagen_proyecto:v1.0` automáticamente según la configuración del `docker-compose.yml`.

**Verifica que se creó correctamente:**
```bash
docker images
```

Deberías ver `imagen_proyecto` con tag `v1.0` en la lista.

### Paso B: Sincronizar la Base de Datos (Migraciones)

```bash
docker-compose run web python manage.py migrate
```

Este comando:
- 🔄 Sincroniza el esquema de la base de datos
- 📝 Aplica todas las migraciones pendientes
- ✅ Prepara la BD para usar el proyecto

### Paso C: Crear Superusuario (Administrador)

```bash
docker-compose run web python manage.py createsuperuser
```

Te pedirá:
- **Username:** Tu nombre de usuario admin
- **Email:** Tu correo
- **Password:** Tu contraseña (escondida al escribir)
- **Password (again):** Confirmar contraseña

### Paso 2: Iniciar el Servidor

```bash
docker-compose up
```

**Verás algo como:**
```
Starting modelobaseweb_web_1 ... done
Starting modelobaseweb_db_1 ... done
Starting modelobaseweb on port 3000...
```

**Accede a tu sitio:** http://localhost:3000

**Panel de administración:** http://localhost:3000/admin (usa tus credenciales del superusuario)

---

## Estructura del Proyecto

```
modeloBaseWeb/
├──proyecto
|    ├──proyectoDjango
|    │   ├── settings.py         # Configuración del proyecto
|    │   ├── urls.py             # Rutas principales
|    │   ├── wsgi.py             # Interfaz WSGI
|    │   └── asgi.py             # Interfaz ASGI
|    |
|    ├── web/                    # Tu primera aplicación Django
|    |   ├── migrations/         # Historial migraciones de la base de datos
|    |   |   └──_init_.py        #
|    |   ├── static/             # Archivos estáticos (CSS, JS, imágenes)
|    |   |   └── ...             # carpetas: css, files, fonts, icons, img, js, media
|    |   ├── templates/          # Plantillas de HTML
|    |   |   └── includes        # plantillas herencias
|    |   ├── admin.py            # Panel administrativo
|    |   ├── apps.py             # 
|    │   ├── models.py           # Modelos de BD
|    |   ├── tests.py            # 
|    │   ├── urls.py             # Rutas de la app
|    │   └── views.py            # Lógica de negocio
|    |
|    ├── docker-compose.yml      # Orquestación de servicios
|    ├── Dockerfile              # Configuración del contenedor
|    ├── manage.py               # Archivo principal de Django
|    ├── requirements.txt        # Dependencias a instalar
|    ├── .gitignore              # Archivos a ignorar en git
|    ├── README.md               # Este archivo

```

---

## 📖 Documentación Completa

Para una guía **paso a paso** detallada, consulta:
→ [**GUIA.MD**](./GUIA.MD)

En esta guía encontrarás:
- **FASE 1** → Estructura básica (Django + Docker)
- **FASE 2** → Crear tu primera página web funcional
- **FASE 3** → Docker-Compose para proyectos profesionales

---

## 🛠️ Tecnologías Incluidas

| Tecnología | Descripción |
|-----------|-----------|
| **Django 4.2+** | Framework web de alto nivel en Python |
| **Docker** | Contenerización para desarrollo consistente |
| **Python 3.10+** | Lenguaje de programación |

---

## 🔧 Configuración Avanzada

### Usando Docker Compose (Recomendado)

```bash
docker-compose up --build
```

**Esto levanta automáticamente:**
- ✅ Servidor Django (puerto 3000)
- ✅ Base de datos PostgreSQL
- ✅ Nginx como proxy inverso (puerto 80)
- ✅ Volúmenes persistentes para datos

### Flujo Alterno (Si necesitas hacer cambios en el código)

**Terminal 1 - Inicia el servidor:**
```bash
docker-compose up
```

**Terminal 2 - Ejecuta comandos en paralelo:**
```bash
# Hacer migraciones mientras el servidor corre
docker-compose exec web python manage.py makemigrations

# Aplicar migraciones
docker-compose exec web python manage.py migrate

# Ver logs
docker-compose logs -f web
```

### Variables de Entorno

Crea un archivo `.env` en la raíz del proyecto:

```env
DEBUG=False
SECRET_KEY=tu-clave-secreta-aqui
DATABASE_URL=postgres://user:password@db:5432/modelobaseweb
ALLOWED_HOSTS=localhost,127.0.0.1,tudominio.com
```

---

## 📋 Comandos Útiles Diarios

### Iniciar/Detener el Servidor

```bash
# Iniciar en foreground (ver logs en tiempo real)
docker-compose up

# Iniciar en background (modo daemon)
docker-compose up -d

# Detener el servidor
docker-compose down

# Ver logs en tiempo real
docker-compose logs -f web
```

### Trabajar con la Base de Datos

```bash
# Crear migraciones (después de cambios en models.py)
docker-compose exec web python manage.py makemigrations

# Aplicar migraciones pendientes
docker-compose exec web python manage.py migrate

# Ver estado de las migraciones
docker-compose exec web python manage.py showmigrations
```

### Administración del Proyecto

```bash
# Crear nuevo superusuario
docker-compose exec web python manage.py createsuperuser

# Acceder a la shell interactiva de Django
docker-compose exec web python manage.py shell

# Ejecutar tests
docker-compose exec web python manage.py test

# Recolectar archivos estáticos
docker-compose exec web python manage.py collectstatic --noinput
```

### Mantenimiento del Contenedor

```bash
# Reconstruir la imagen (sin caché)
docker-compose build --no-cache

# Eliminar contenedores y volúmenes (⚠️ Elimina datos)
docker-compose down -v

# Ver estado de servicios
docker-compose ps

# Entrar en bash del contenedor
docker-compose exec web bash
```

---

## 🌱 Próximos Pasos

Una vez tengas el proyecto corriendo:

1. **Personaliza las vistas** — Edita `myapp/views.py`
2. **Diseña tus templates** — Crea HTML en `myapp/templates/`
3. **Define tus modelos** — Estructura tu base de datos en `myapp/models.py`
5. **Desplega en producción** — Usa Docker Compose en tu servidor

---

## 🤝 Contribuciones

¿Tienes mejoras o sugerencias para la plantilla?

**¡Te invito a colaborar!**

- 🐛 **Reportar bugs** — [Issues](https://github.com/evidadeusto/modeloBaseWeb/issues)
- 🔀 **Hacer pull requests** — Tus contribuciones son bienvenidas

---

## 📄 Licencia

Este proyecto se distribuye bajo la licencia **MIT**. Eres libre de usar, modificar y distribuir el código, siempre que mantengas la mención de la licencia original.

---
⭐ **Si este proyecto te es útil, ayuda a otros dejando una estrella en GitHub** ⭐

---
## 💬 Conecta Conmigo

¿Preguntas, sugerencias o simplemente quieres compartir cómo usas esta plantilla?

💼 **LinkedIn:** [Juliam Guerrero Diaz](https://www.linkedin.com/in/juliamguerrero/)

📧 **Email:** [juliamdario.g@deusto.es](mailto:juliamdario.g@deusto.es)

🐙 **GitHub:** [@JULIAMGUERRERO](https://github.com/JULIAMGUERRERO)