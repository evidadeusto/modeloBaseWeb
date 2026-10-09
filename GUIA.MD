# GUÍA: Creacion de Sitio Web Profesional

## ¿Qué vas a aprender?

Esta guía te enseña a crear un sitio web profesional usando **Django** (un framework Python) y **Docker** (contenedores). 

> **NOTA:** No necesitas experiencia previa en programación.

**Esta guia incluye 3 fases, en ellas aprenderás:**
1. **FASE 1** → Configurar el ambiente basico (Django + Docker)
2. **FASE 2** → Crear tu primera página web funcional
3. **FASE 3** → Crear un proceso más fácil con el uso de docker-compose.

### Requisitos en software

Antes de empezar, asegúrate de tener:

- **Sistema Operativo:** Windows, mac0S o Linux
- **[Docker Desktop instalado](https://www.docker.com/products/docker-desktop).** Descarga e instala. (Caso especial para macOS, recibirán una solicitud de instalar Rosetta 2 automáticamente, y que es necesario.)
- **[Visual Studio Code instalado](https://code.visualstudio.com/download)** (editor de código)


### 📑 Índice rápido
- [FASE 1: Estructura básica](#-fase-1-de-3-estructura-basica-del-proyecto)
- [FASE 2: Página web funcional](#-fase-2-de-3-crear-tu-página-web-funcional)
- [FASE 3: Docker-Compose profesional](#-fase-3-de-3-docker-compose-para-sistemas-profesionales-completos)
- [Glosario](#-glosario-completo---términos-clave) 

---

# 📁 FASE 1 DE 3: Estructura Basica del Proyecto

## PASO 0: Preparación previa

### ✅ Paso A: Verificar que Docker está instalado

Abre una terminal/PowerShell y ejecuta:

```Bash
docker --version
docker-compose --version
```

**Deberías ver algo como:**
```
Docker version 24.0.0
Docker Compose version v2.20.0
```

Si no aparecen, descarga e instala [Docker Desktop](https://www.docker.com/products/docker-desktop) primero.

---

### (OPCIONAL) Validar Docker con tu primer contenedor

Para asegurar que todo funciona correctamente, ejecuta este comando de prueba:

```bash
docker run hello-world
```

**¿Qué va a pasar?**
- Docker descargará una pequeña imagen de prueba
- Creará un contenedor y lo ejecutará
- Mostrará un mensaje de bienvenida

**Verás esto en la terminal:**
```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

**¿Por qué es útil?** 
✅ Valida que Docker funciona sin problemas  
✅ Prueba la conexión a internet (descarga la imagen)  
✅ Cachea la imagen para futuras pruebas (más rápido)  
✅ Te da confianza de que todo está listo  

> **Nota:** Este paso es opcional pero **RECOMENDADO**. Si no quieres hacerlo, salta directamente al Paso B.

---

### ✅ Paso B: Crear carpeta del proyecto

**En Windows:**
1. Abre el Explorador de Archivos
2. Ve a la ubicación donde quieras tu proyecto (por ejemplo, `Documentos`)
3. Click derecho → Nueva carpeta → Nómbrala `proyecto`
4. Click derecho en `proyecto` → "Abrir en terminal" o "Open PowerShell here"

**En Mac:**
1. Abre Finder
2. Ve a Documentos (o la carpeta que prefieras)
3. Click derecho → Nueva carpeta → Nómbrala `proyecto`
4. Abre Terminal (Aplicaciones → Utilidades → Terminal)
5. Escribe: `cd ~/Documents/proyecto` (ajusta la ruta si es diferente)

**En Linux:**
1. Abre el gestor de archivos (Nautilus, Dolphin, etc.)
2. Ve a tu carpeta preferida (por ejemplo, Documentos)
3. Click derecho → Crear carpeta → Nómbrala `proyecto`
4. Click derecho en `proyecto` → "Abrir terminal aquí"
5. O abre terminal y escribe: `cd ~/Documentos/proyecto` (ajusta según tu carpeta)

---

### ✅ Paso C: Abrir la carpeta en Visual Studio Code

1. Abre Visual Studio Code
2. Click en "Archivo" → "Abrir carpeta"
3. Selecciona la carpeta `proyecto` que creaste
4. Click en "Seleccionar carpeta"

**¿Ves la carpeta en el lado izquierdo?** ✅ **¡Perfecto! Continúa con PASO 1.**

---

## PASO 1: Crear Proyecto Django con Docker

### ¿Qué va a pasar?

Vamos a decirle a Docker que execute un comando dentro de un contenedor. Django es un framework (herramienta) que hace más fácil crear sitios web.

### ▶️ Comando a ejecutar

**Selecciona tu Sistema Operativo:**

**Windows (PowerShell):**
```powershell
docker run --rm -v "${PWD}:/usr/src/app" -w /usr/src/app python:3.11-slim sh -c "pip install django && django-admin startproject proyectoDjango ."
```

**macOS / Linux (Bash):**
```bash
docker run --rm -v "$(pwd):/usr/src/app" -w /usr/src/app python:3.11-slim sh -c "pip install django && django-admin startproject proyectoDjango ."
```

> **Nota sobre PWD:** `${PWD}` en PowerShell vs `$(pwd)` en Bash. Ambos significan "carpeta actual". Django crea los mismos archivos.

### ¿Qué hace cada parte del comando?
| Componente | Qué hace |
|-----------|----------|
| `docker run` | Ejecuta un contenedor |
| `--rm` | Lo elimina al terminar |
| `-v "${PWD}:/usr/src/app"` | Monta tu carpeta actual dentro del contenedor |
| `-w /usr/src/app` | Trabaja dentro de ese directorio |
| `python:3.11-slim` | Imagen de Python 3.11 (ligera) |
| `pip install django` | Instala Django |
| `django-admin startproject proyectoDjango .` | Crea el proyecto llamado proyectoDjango |

Y se crea automáticamente esta estructura en tu carpeta:
```
proyecto/
├── manage.py
├── proyectoDjango/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
```

---

## PASO 2: Crear requirements.txt 

### 📝 ¿Qué es requirements.txt?

Es un archivo que en lista **todas las herramientas (paquetes) que tu proyecto necesita**. Son los requerimientos basicos para que otros puedan reproducir tu proyecto.

### ▶️ Opción 1: Terminal (recomendado)

**Windows (PowerShell):**
```powershell
echo Django==5.0 > requirements.txt
```

**macOS / Linux (Bash):**
```bash
echo "Django==5.0" > requirements.txt
```

### Opción 2: Editor de texto

1. Crea un archivo llamado `requirements.txt`
2. Escribe esto adentro:
```
Django==5.0
```
3. Guarda el archivo

### ✅ Verifica que exista en tu carpeta y continúa con PASO 3.

---

## PASO 3: Crear Dockerfile

### 🐳 ¿Qué es Dockerfile?

**Dockerfile** es un archivo de "instrucciones" que le dice a Docker cómo construir tu contenedor. Es como un plano para construir una casa.

### ▶️ Opción 1: Terminal (recomendado)

**Windows (PowerShell)** - Copia todo el bloque:
```powershell
@'
FROM python:3.11-slim

# Evita bytecode y fuerza salida de logs en tiempo real
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Herramientas de compilación para librerías que las necesitan
RUN apt-get update \
    && apt-get install -y --no-install-recommends gcc build-essential \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/src/app

COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 3000

CMD ["python", "manage.py", "runserver", "0.0.0.0:3000"]
'@ | Out-File -FilePath Dockerfile -Encoding utf8
```

**macOS / Linux (Bash)** - Copia todo el bloque:
```bash
cat << 'EOF' > Dockerfile
FROM python:3.11-slim

# Evita bytecode y fuerza salida de logs en tiempo real
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Herramientas de compilación para librerías que las necesitan
RUN apt-get update \
    && apt-get install -y --no-install-recommends gcc build-essential \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/src/app

COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 3000

CMD ["python", "manage.py", "runserver", "0.0.0.0:3000"]
EOF
```

### Opción 2: Editor de texto

1. Crea un archivo llamado `Dockerfile` (sin extensión)
2. Copia y pega este contenido:

```dockerfile
FROM python:3.11-slim

# Evita bytecode y fuerza salida de logs en tiempo real
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Herramientas de compilación para librerías que las necesitan
RUN apt-get update \
    && apt-get install -y --no-install-recommends gcc build-essential \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/src/app

COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 3000

CMD ["python", "manage.py", "runserver", "0.0.0.0:3000"]
```

3. Guarda el archivo como `Dockerfile`

### 📚 Explicación línea por línea
| Línea | Qué hace |
|-------|----------|
| `FROM python:3.11-slim` | Usa imagen de Python 3.11 (pequeña) |
| `ENV PYTHONDONTWRITEBYTECODE=1` | Evita generar archivos `.pyc` (bytecode compilado) - reduce tamaño |
| `ENV PYTHONUNBUFFERED=1` | Fuerza logs en tiempo real sin buffer - mejor debugging en Docker |
| `RUN apt-get update...` | Instala herramientas de compilación (gcc, build-essential) necesarias para librerías Python complejas |
| `rm -rf /var/lib/apt/lists/*` | Limpia cache de apt después de instalar - reduce imagen en ~100MB |
| `WORKDIR /usr/src/app` | Crea directorio de trabajo **siguiendo convención Unix profesional.**  |
| `COPY requirements.txt .` | Copia requirements.txt al contenedor |
| `RUN pip install --no-cache-dir --upgrade pip` | Actualiza pip y evita cachear dependencias - reduce imagen en ~50-100MB |
| `RUN pip install --no-cache-dir -r requirements.txt` | Instala dependencias sin guardar cache |
| `COPY . .` | Copia todo el código del proyecto |
| `EXPOSE 3000` | Abre puerto 3000 |
| `CMD ["python", "manage.py", "runserver", "0.0.0.0:3000"]` | Comando que se ejecuta al iniciar el contenedor |

---

## PASO 4: Construir la imagen

### Compilar el Dockerfile

Ejecuta este comando:

```powershell
docker build -t imagen_proyecto:v1.0 .
```

### 📚 Desglose del comando

| Parte | Qué significa |
|-------|---------------|
| `docker build` | Compila el Dockerfile automáticamente |
| `-t` | Asigna un nombre y etiqueta (tag) a la imagen |
| `imagen_proyecto` | **Nombre** de la imagen (identificador principal) |
| `v1.0` | **Tag** de la imagen (versión o variante) |
| `.` | Busca el Dockerfile en la carpeta actual |

### ¿Qué diferencia hay entre nombre y tag?

```
imagen_proyecto:v1.0

nombre ↓          ↓ tag
  
Nombre = Identificador único de la imagen
Tag = Versión o variante de esa imagen

Ejemplo con versiones:
- contenedor_proyecto:v1.0
- contenedor_proyecto:v2.0
- contenedor_proyecto:produccion
- contenedor_proyecto:desarrollo
```

### ✅ Beneficios de usar nombres y tags

- ✅ Puedes tener múltiples versiones de la misma imagen
- ✅ Identificas rápidamente qué versión usas
- ✅ Útil para cambiar entre desarrollo y producción
- ✅ Facilita el control de cambios

### ¿Cuánto tarda?

**Primera vez:** ~2-3 minutos (descarga dependencias)  
**Siguientes veces:** Más rápido (usa caché)

## PASO 5: Verificar que la imagen se creó 

### ✅ Confirmación

Ejecuta este comando para ver tus imágenes:

```powershell
docker images
```

Deberías ver `contenedor_proyecto` con tag `sitio_web` en la lista, si no creaste imagenes previamente sera la unica que aparecera en lista.

---

## PASO 6: Ejecutar migraciones - Crear base de datos 

### ¿Qué son las migraciones?

Las **migraciones** son cambios organizados en tu base de datos. Es como un "historial de cambios" que Django controla automáticamente.

### ▶️ Comando

**Windows (PowerShell):**
```powershell
docker run --rm -v "${PWD}:/usr/src/app" -w /usr/src/app imagen_proyecto:v1.0 python manage.py migrate
```

**macOS / Linux (Bash):**
```bash
docker run --rm -v "$(pwd):/usr/src/app" -w /usr/src/app imagen_proyecto:v1.0 python manage.py migrate
```


### Explicación del comando
| Componente | Qué hace |
|-----------|----------|
| `docker run` | Ejecuta un contenedor |
| `--rm` | Elimina el contenedor después de terminar |
| `-v "${PWD}:/usr/src/app"` | Sincroniza tu carpeta actual con `/usr/src/app` del contenedor |
| `-w /usr/src/app` | Establece el directorio de trabajo |
| `imagen_proyecto:v1.0` | Usa la imagen que creaste |
| `python manage.py migrate` | Ejecuta las migraciones de Django |

### ¿Qué resultado obtiene?
- ✅ Crea la base de datos SQLite (`db.sqlite3`)
- ✅ Genera todas las tablas necesarias para Django
- ✅ **Sin esto, el admin no funcionará**

---

## PASO 7: Crear superusuario - Administrador 

### ¿Qué es un superusuario?

Un **superusuario** es un usuario administrador con permisos totales. Usarás esto para acceder al panel de control de Django.

### ▶️ Comando (será interactivo)

**Windows (PowerShell):**
```powershell
docker run --rm -it -v "${PWD}:/usr/src/app" -w /usr/src/app imagen_proyecto:v1.0 python manage.py createsuperuser
```

**macOS / Linux (Bash):**
```bash
docker run --rm -it -v "$(pwd):/usr/src/app" -w /usr/src/app imagen_proyecto:v1.0 python manage.py createsuperuser
```

### Explicación del comando
| Componente | Qué hace |
|-----------|----------|
| `docker run` | Ejecuta un contenedor |
| `--rm` | Elimina el contenedor después de terminar |
| `-i` | Modo interactivo (entrada stdin) |
| `-t` | Asigna pseudo-terminal |
| `-v "${PWD}:/usr/src/app"` | Sincroniza carpeta actual con `/usr/src/app` |
| `-w /usr/src/app` | Establece directorio de trabajo |
| `imagen_proyecto:v1.0` | Usa la imagen creada |
| `python manage.py createsuperuser` | Crea un usuario administrador |

### ¿Qué resultado obtiene?
- ✅ Te pide: usuario, email y contraseña
- ✅ Crea el usuario administrador
- ⚠️ **Guarda bien estos datos** - los usarás para acceder al admin y tener acceso del panel principal.

---

## PASO 8: Iniciar servidor - Poner en línea 
### ¿Qué va a pasar?

Tu sitio web estará disponible en `http://localhost:3000` (solo en tu PC de manera Local).

> **NOTA:** Estos comandos son largos porque incluyen todas las opciones (`-v`, `-w`, `-p`). En **FASE 3** aprenderás a simplificarlos con `docker-compose.yml`. Por ahora, entiende cada parámetro para aprender cómo funciona Docker realmente. 

### ▶️ Comando

**Windows (PowerShell):**
```powershell
docker run -p 3000:3000 -v "${PWD}:/usr/src/app" -w /usr/src/app imagen_proyecto:v1.0 python manage.py runserver 0.0.0.0:3000
```

**macOS / Linux (Bash):**
```bash
docker run -p 3000:3000 -v "$(pwd):/usr/src/app" -w /usr/src/app imagen_proyecto:v1.0 python manage.py runserver 0.0.0.0:3000
```

### Explicación del comando
| Componente | Qué hace |
|-----------|----------|
| `docker run` | Ejecuta un contenedor |
| `-p 3000:3000` | Mapea puerto 3000 PC → puerto 3000 contenedor |
| `-v "${PWD}:/usr/src/app"` | Sincroniza tu carpeta actual con `/usr/src/app` |
| `-w /usr/src/app` | Establece directorio de trabajo |
| `imagen_proyecto:v1.0` | Usa la imagen creada |
| `python manage.py runserver` | Inicia el servidor Django |
| `0.0.0.0:3000` | Escucha en todos los interfaces en puerto 3000 |

### ¿Qué resultado obtiene?
- ✅ Django corre en **http://localhost:3000**
- ✅ Cambios en archivos se detectan automáticamente
- ⏹️ Para detener: presiona `Ctrl + C`

---

## PASO 9: Acceder al panel de administración

### 🎛️ ¿Qué es el panel admin?

Es una interfaz donde puedes gestionar tu sitio web sin escribir código. Viene incluida con Django automáticamente.

### ▶️ Pasos

En el navegador ve a:
```
http://localhost:3000/admin/
```

Ingresa con:
- **Usuario:** (el que creaste en PASO 7)
- **Contraseña:** (la que creaste en PASO 7)

✅ **¡Panel admin listo para usar!**

---

## ✅ Estado final - FASE 1 completada

Después de completar los 9 pasos, tu carpeta debería verse así:

```
proyecto/
├── manage.py                  ← ✅ PASO 1
├── requirements.txt           ← ✅ PASO 2
├── Dockerfile                 ← ✅ PASO 3
├── db.sqlite3                 ← ✅ PASO 6 (base de datos)
└── proyectoDjango/
    ├── settings.py           ← ✅ PASO 1
    ├── urls.py               ← ✅ PASO 1
    ├── asgi.py               ← ✅ PASO 1
    ├── wsgi.py               ← ✅ PASO 1
    └── __init__.py           ← Configuración interna
```

---

# 📁 FASE 2 DE 3: Crear Tu Página Web Funcional

> **En esta fase:** Construiremos tu primer sitio web **completamente funcional** con navbar, múltiples páginas y estilos profesionales.

### Lo que vamos a crear:

```
Tu sitio web final se verá así:

┌─────────────────────────────────────┐
│ Mi Sitio Web                        │  ← Header
│ HOME | PLANTILLA 1 | PLANTILLA 2... │
├─────────────────────────────────────┤
│                                     │
│  Contenido de la página actual      │  ← Main
│                                     │
├─────────────────────────────────────┤
│ © 2026 Mi Sitio Web                 │  ← Footer
└─────────────────────────────────────┘

```

### 15 pasos simples:

1. **PASOS 1-6:** Preparar la app (crear, registrar, carpetas, rutas, vistas)
2. **PASOS 7-11:** Crear componentes (header, footer, base, CSS, JavaScript)
3. **PASOS 12-13:** Crear páginas (home + 4 plantillas)
4. **PASO 14:** Configurar Django (settings.py)
5. **PASO 15:** Ver en navegador y probar

## PASO 1: Crear la app `web`

### ¿Qué es una "app" en Django?

Una **app** es como un componente o módulo dentro de tu proyecto, es simplemente una forma de organizar tu código por temas dentro del mismo programa. Donde guardarás:
- ✅ Tus páginas web (templates HTML)
- ✅ La lógica que procesa datos (views)
- ✅ Los diseños visuales (CSS)
- ✅ Las imágenes y archivos

Puedes tener varias apps en un proyecto. En nuestro caso, crearemos una app principal llamada `web/`.

### ▶️ Comando para crear la app

**Windows (PowerShell):**
```powershell
docker run --rm -v "${PWD}:/usr/src/app" -w /usr/src/app imagen_proyecto:v1.0 python manage.py startapp web
```

**macOS/Linux (Bash):**
```bash
docker run --rm -v "$(pwd):/usr/src/app" -w /usr/src/app imagen_proyecto:v1.0 python manage.py startapp web
```

### ¿Qué crea Django?

Se generará automáticamente esta carpeta:

```
web/
├── migrations/          ← Historial de cambios en base de datos
│   └── __init__.py
├── __init__.py
├── admin.py            ← Registra modelos en panel admin
├── apps.py             ← Configuración de la app
├── models.py           ← Estructura de datos (tablas BD)
├── tests.py            ← Pruebas automáticas
└── views.py            ← Lógica de tu sitio web ⭐
```

**¡Perfecto! Continúa con PASO 2.**

---

## PASO 2: Registrar la app en Django

### ¿Por qué es necesario?

Django necesita "conocer" todas tus apps. Si no la registras, Django la ignora completamente.

### ▶️ Edita el archivo `proyectoDjango/settings.py`

1. Abre el archivo en VS Code
2. Busca la sección llamada `INSTALLED_APPS` (alrededor de la línea 33)
3. Debería verse así:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

4. **Agrega `'web',` al final (antes del último corchete):**

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'web',  ← ✅ AGREGAR ESTA LÍNEA
]
```

5. **Guarda el archivo** (Ctrl+S o Cmd+S)

✅ **¡Listo! Continúa con PASO 3.**

---

## PASO 3: Crear carpetas para templates y archivos estáticos

### 📁 ¿Qué vamos a crear?

Tu sitio web necesita una estructura de carpetas bien organizada:

**templates/** → Archivos HTML (las páginas)
- `base.html` → Plantilla base (estructura común)
- `home.html` → Página de inicio
- `includes/` → Componentes reutilizables

**static/** → Estilos, scripts e imágenes
- `css/` → Estilos CSS
- `js/` → Scripts JavaScript
- `img/` → Imágenes
- Y otros recursos...

### 📚 ¿Por qué esta estructura?

**DRY** (Don't Repeat Yourself) → No repites código
- ✅ Header y footer en 1 archivo (`includes/`) 
- ✅ Se usan en todas las páginas con `{% include %}`
- ✅ Si cambias el diseño, cambias en 1 lugar

### ▶️ En Windows (PowerShell)

Copia y pega estos comandos uno por uno:

```powershell
mkdir web\templates
mkdir web\templates\includes
mkdir web\static\css
mkdir web\static\js
mkdir web\static\img
mkdir web\static\icons
mkdir web\static\files
mkdir web\static\fonts
mkdir web\static\media
mkdir web\static\media\audio
mkdir web\static\media\video
```

### ▶️ En macOS/Linux

Abre Terminal en tu carpeta de proyecto y ejecuta:

```bash
mkdir -p web/templates/includes
mkdir -p web/static/css
mkdir -p web/static/js
mkdir -p web/static/img
mkdir -p web/static/icons
mkdir -p web/static/files
mkdir -p web/static/fonts
mkdir -p web/static/media/audio
mkdir -p web/static/media/video
```

> **Nota:** El parámetro `-p` en macOS/Linux crea todos los directorios anidados de una vez.

### ✅ Verificación

En VS Code, deberías ver la estructura así en el panel izquierdo:

```
web/
├── templates/
│   └── includes/         
├── static/
│   ├── css/
│   ├── js/
│   ├── img/
│   ├── icons/
│   └── media/
└── (otros archivos...)
```

✅ **Continúa con PASO 4.**

---

## PASO 4: Crear el archivo de rutas `web/urls.py`

### 🔗 ¿Qué es un archivo de rutas?

Es como un "mapa de direcciones" de tu sitio web. Define qué página se muestra cuando alguien accede a cada URL.

### ▶️ Opción 1: Crear con terminal (recomendado)

**En Windows (PowerShell):**
```powershell
New-Item web\urls.py -ItemType File
```

**En macOS/Linux:**
```bash
touch web/urls.py
```

### Opción 2: Crear manualmente en VS Code

1. Click derecho en la carpeta `web/`
2. "New File" → escribe `urls.py`

### ▶️ Ahora agrega este contenido

Abre `web/urls.py` y copia-pega esto:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
    path('plantilla1/', views.plantilla1, name='plantilla1'),
    path('plantilla2/', views.plantilla2, name='plantilla2'),
    path('plantilla3/', views.plantilla3, name='plantilla3'),
    path('plantilla4/', views.plantilla4, name='plantilla4'),
]
```

### 📚 Explicación:
- `path('', ...)` → URL raíz (http://localhost:3000/)
- `path('plantilla1/', ...)` → URL para plantilla 1 (http://localhost:3000/plantilla1/)
- `path('plantilla2/', ...)` → URL para plantilla 2 (http://localhost:3000/plantilla2/)
- Y así con las otras...

### **Importante:**
- `name='plantilla1'` → Este nombre se usa en el header con `{% url 'plantilla1' %}`
- Debe coincidir exactamente con las funciones en `views.py`

**Guarda el archivo y continúa con PASO 5.**

---

## PASO 5: Conectar las rutas al proyecto

### ¿Por qué?

Así Django sabe que debe usar las rutas de tu app `web/`.

### ▶️ Edita `proyectoDjango/urls.py`

1. Abre el archivo `proyectoDjango/urls.py`
2. Busca el contenido actual (debería verse así):

```python
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

3. **Modifica a esto:**

```python
from django.contrib import admin
from django.urls import path, include  ← AGREGAR: ", include"

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('web.urls')),  ← AGREGAR ESTA LÍNEA NUEVA
]
```

### 📚 Explicación:
- `include('web.urls')` → "Importa todas las rutas del archivo `web/urls.py`"
- `path('', ...)` → "Usa esas rutas en la raíz del sitio"

**Guarda el archivo y continúa con PASO 6.**

---

## PASO 6: Crear las Vistas en `web/views.py`

### ¿Qué es una vista (view)?

Una **vista** es una función Python que:
1. **Recibe** una solicitud del navegador
2. **Procesa** datos
3. **Devuelve** una página HTML con datos

### 📁 Archivo donde guardar:
```
web/views.py  ← AQUÍ VA TODO
```

### ▶️ Reemplaza TODO el contenido de `web/views.py` con esto:

```python
from django.shortcuts import render

def home(request):
    """Vista de página de inicio"""
    context = {
        'titulo': '¡Bienvenido a tu sitio web!',
        'mensaje': 'Esta es tu primera página creada con Django y Docker',
    }
    return render(request, 'home.html', context)

def plantilla1(request):
    """Vista de plantilla 1"""
    context = {
        'titulo': 'Plantilla 1',
        'descripcion': 'Primera página de ejemplo',
        'contenido': 'Aquí puedes agregar tu contenido...',
    }
    return render(request, 'plantilla1.html', context)

def plantilla2(request):
    """Vista de plantilla 2"""
    context = {
        'titulo': 'Plantilla 2',
        'descripcion': 'Segunda página de ejemplo',
        'contenido': 'Aquí puedes agregar tu contenido...',
    }
    return render(request, 'plantilla2.html', context)

def plantilla3(request):
    """Vista de plantilla 3"""
    context = {
        'titulo': 'Plantilla 3',
        'descripcion': 'Tercera página de ejemplo',
        'contenido': 'Aquí puedes agregar tu contenido...',
    }
    return render(request, 'plantilla3.html', context)

def plantilla4(request):
    """Vista de plantilla 4"""
    context = {
        'titulo': 'Plantilla 4',
        'descripcion': 'Cuarta página de ejemplo',
        'contenido': 'Aquí puedes agregar tu contenido...',
    }
    return render(request, 'plantilla4.html', context)
```

### 📝 Explicación simple:

Cada función:
- ✅ Recibe una solicitud (`request`)
- ✅ Crea un diccionario `context` con datos
- ✅ Devuelve el HTML renderizado con `render()`

**En el HTML accederás a los datos con:**
- `{{ titulo }}`
- `{{ descripcion }}`
- `{{ contenido }}`

### 🎯 ¿Qué es `context`?

Es el "puente" entre Python (backend) y HTML (frontend):

```
Python (views.py)           HTML (templates)
context = {
    'titulo': '...'    →    {{ titulo }}
    'mensaje': '...'   →    {{ mensaje }}
}
```

**Guarda el archivo y continúa con PASO 7.**

---

## PASO 7: Crear el Header con Navbar Profesional

### ¿Qué vamos a hacer?

Crearemos un header con:
- 📌 Título y subtítulo centrados
- 🔗 Menú de navegación con links
- 📱 Menú hamburguesa (que aparece en móvil)

### 📁 Carpeta donde guardar:
```
web/templates/includes/header.html  ← AQUÍ VA ESTE ARCHIVO
```

### ▶️ Crea el archivo `header.html`

En VS Code:
1. Click derecho en la carpeta `web/templates/includes/`
2. "New File" → `header.html`

### ▶️ Copia y pega este código:

```html
<!-- Header Component - Componente de encabezado con navbar -->
<header class="header">
    <!-- Sección del título y subtítulo (centrados) -->
    <div class="header-intro">
        <div class="container">
            <h1>🚀 Mi Sitio Web</h1>
            <p class="subtitle">Creado con Django y Docker</p>
        </div>
    </div>
    
    <!-- Sección de Navegación -->
    <div class="header-navbar">
        <div class="container navbar-container">
            <!-- Menú Hamburguesa (solo visible en móvil) -->
            <button class="hamburger" id="hamburger" aria-label="Menú">
                <span></span>
                <span></span>
                <span></span>
            </button>
            
            <!-- Menú de Navegación -->
            <nav class="navbar" id="navbar">
                <ul class="nav-menu">
                    <li><a href="{% url 'home' %}" class="nav-link">HOME</a></li>
                    <li><a href="{% url 'plantilla1' %}" class="nav-link">PLANTILLA 1</a></li>
                    <li><a href="{% url 'plantilla2' %}" class="nav-link">PLANTILLA 2</a></li>
                    <li><a href="{% url 'plantilla3' %}" class="nav-link">PLANTILLA 3</a></li>
                    <li><a href="{% url 'plantilla4' %}" class="nav-link">PLANTILLA 4</a></li>
                </ul>
            </nav>
        </div>
    </div>
</header>
```

### 🔍 ¿Qué hace cada parte?

| Elemento | Función |
|----------|---------|
| `header-intro` | Título + Subtítulo en el centro |
| `header-navbar` | Contenedor del menú |
| `hamburger` | Botón ☰ (solo aparece en móvil) |
| `navbar` | Menú horizontal de navegación |
| `nav-menu` | Lista de enlaces (HOME, PLANTILLA 1, etc) |

### 📝 IMPORTANTE:
- `{% url 'home' %}` → Genera el link a la página de inicio
- `{% url 'plantilla1' %}` → Genera el link a plantilla 1
- Estos links funcionarán cuando cremos las rutas en `urls.py`

**Guarda el archivo y continúa con PASO 8.**

---

## PASO 8: Crear el Footer

### Carpeta donde guardar:
```
web/templates/includes/footer.html  ← AQUÍ VA ESTE ARCHIVO
```

### ▶️ Crea el archivo `footer.html`

En VS Code:
1. Click derecho en `web/templates/includes/`
2. "New File" → `footer.html`

### ▶️ Copia y pega:

```html
<!-- Footer Component - Componente de pie de página -->
<footer class="footer">
    <p>&copy; 2026 Mi Sitio Web. Todos los derechos reservados.</p>
    <p><small>Creado con ❤️ usando Django y Docker</small></p>
</footer>
```

**Guarda y continúa con PASO 9.**

---

## PASO 9: Crear el Template Base `base.html`

### La estructura que usa toda tu página

### Carpeta donde guardar:
```
web/templates/base.html  ← AQUÍ VA ESTE ARCHIVO
```

### ▶️ Crea el archivo `base.html`

### ▶️ Copia y pega:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}Mi Sitio Web{% endblock %}</title>
    {% load static %}
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
    <!-- Incluir el componente header -->
    {% include "includes/header.html" %}

    <!-- Contenido específico de cada página -->
    <main class="container">
        {% block content %}
        <!-- Aquí va el contenido específico de cada página -->
        {% endblock %}
    </main>

    <!-- Incluir el componente footer -->
    {% include "includes/footer.html" %}
    
    <!-- Script del menú hamburguesa -->
    {% load static %}
    <script src="{% static 'js/menu.js' %}"></script>
</body>
</html>
```

### 📝 Importante:
- `{% include %}` → Inyecta header.html y footer.html aquí
- `{% block content %}` → Cada página llena esta sección
- `<script src="{% static 'js/menu.js' %}">` → Agrega interactividad al menú

**Guarda y continúa con PASO 10.**

---

## PASO 10: Crear los Estilos CSS del Navbar y del Sitio

### Aquí hacemos el diseño visual.

### 📁 Carpeta donde guardar:
```
web/static/css/style.css  ← AQUÍ VA ESTE ARCHIVO
```

### Crea el archivo `style.css`

En VS Code:
1. Click derecho en `web/static/css/`
2. "New File" → `style.css`

### ▶️ Copia y pega TODO este CSS:

<details>
<summary>✨ Click para ver/copiar el CSS completo</summary>

```css
/* ==================== RESET Y GENERALES ==================== */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html, body {
    height: 100%;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    line-height: 1.6;
    color: #333;
    background-color: #f8f9fa;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    width: 100%;
}

/* ==================== HEADER ==================== */
.header {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    flex-shrink: 0;
}

.header-intro {
    padding: 40px 0;
    text-align: center;
    background: rgba(0, 0, 0, 0.05);
}

.header-intro h1 {
    font-size: 2.5em;
    margin: 0 0 15px 0;
}

.header-intro .subtitle {
    font-size: 1.1em;
    opacity: 0.9;
    margin: 0;
}

.header-navbar {
    padding: 15px 0;
    background: rgba(0, 0, 0, 0.1);
}

.navbar-container {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    gap: 30px;
}

/* ==================== NAVBAR ==================== */
.navbar {
    display: flex;
}

.nav-menu {
    display: flex;
    list-style: none;
    gap: 30px;
    margin: 0;
    padding: 0;
}

.nav-link {
    color: white;
    text-decoration: none;
    font-weight: 500;
    font-size: 0.95em;
    transition: all 0.3s ease;
    position: relative;
}

.nav-link:hover {
    color: #ffd700;
}

.nav-link::after {
    content: '';
    position: absolute;
    bottom: -5px;
    left: 0;
    width: 0;
    height: 2px;
    background-color: #ffd700;
    transition: width 0.3s ease;
}

.nav-link:hover::after {
    width: 100%;
}

/* ==================== HAMBURGUESA ==================== */
.hamburger {
    display: none;
    flex-direction: column;
    background: none;
    border: none;
    cursor: pointer;
    padding: 10px;
    gap: 5px;
}

.hamburger span {
    width: 25px;
    height: 3px;
    background-color: white;
    border-radius: 2px;
    transition: all 0.3s ease;
}

.hamburger.active span:nth-child(1) {
    transform: rotate(45deg) translate(10px, 10px);
}

.hamburger.active span:nth-child(2) {
    opacity: 0;
}

.hamburger.active span:nth-child(3) {
    transform: rotate(-45deg) translate(8px, -8px);
}

/* ==================== MAIN CONTENT ==================== */
main {
    flex: 1;
    padding: 40px 0;
    width: 100%;
}

.welcome {
    background: white;
    padding: 40px;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.welcome h2 {
    color: #667eea;
    font-size: 2em;
    margin-bottom: 15px;
}

.welcome .lead {
    font-size: 1.2em;
    color: #555;
    margin-bottom: 30px;
}

/* ==================== INFO BOXES ==================== */
.info-box,
.next-steps {
    background: #f0f4ff;
    padding: 25px;
    margin: 20px 0;
    border-left: 4px solid #667eea;
    border-radius: 4px;
}

.info-box h3,
.next-steps h3 {
    color: #667eea;
    margin-bottom: 15px;
    font-size: 1.3em;
}

.info-box ul {
    list-style: none;
    padding-left: 0;
}

.info-box li {
    padding: 8px 0;
    font-size: 1.05em;
}

.next-steps ol {
    margin-left: 20px;
}

.next-steps li {
    padding: 8px 0;
    font-size: 1.05em;
}

/* ==================== FOOTER ==================== */
.footer {
    background: #333;
    color: white;
    text-align: center;
    padding: 30px;
    font-size: 0.95em;
    flex-shrink: 0;
    width: 100%;
}

.footer p {
    margin: 5px 0;
}

/* ==================== RESPONSIVE - TABLETS (768px) ==================== */
@media (max-width: 768px) {
    .header-intro h1 {
        font-size: 1.8em;
    }
    
    .header-intro .subtitle {
        font-size: 0.95em;
    }
    
    .hamburger {
        display: flex;
    }
    
    .navbar {
        position: absolute;
        top: 100%;
        left: 0;
        width: 100%;
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        max-height: 0;
        overflow: hidden;
        transition: max-height 0.3s ease;
    }
    
    .navbar.active {
        max-height: 300px;
    }
    
    .nav-menu {
        flex-direction: column;
        gap: 0;
        padding: 20px 0;
    }
    
    .nav-link {
        display: block;
        padding: 12px 20px;
        font-size: 0.95em;
    }
    
    .nav-link::after {
        display: none;
    }
    
    .nav-link:hover {
        background: rgba(0, 0, 0, 0.1);
        color: #ffd700;
    }
    
    .header-navbar {
        position: relative;
        padding: 12px 0;
    }
    
    main {
        padding: 25px 0;
    }
    
    .welcome {
        padding: 25px;
    }
    
    .welcome h2 {
        font-size: 1.5em;
    }
}

/* ==================== RESPONSIVE - MÓVILES PEQUEÑOS (480px) ==================== */
@media (max-width: 480px) {
    body {
        font-size: 14px;
    }
    
    .header-intro h1 {
        font-size: 1.5em;
    }
    
    .hamburger span {
        width: 20px;
        height: 2.5px;
    }
}
```

</details>

### Qué hace este CSS:
- ✅ Estilo bonito para el header (gradiente morado)
- ✅ Navbar horizontal en desktop
- ✅ Hamburguesa visible en móvil
- ✅ Animaciones suaves (hover, transitions)
- ✅ Responsive en tablet y móvil

**Guarda y continúa con PASO 11.**

---

## PASO 11: Crear el JavaScript del Menú Hamburguesa

### Ahora hacemos que el menú sea interactivo

### Carpeta donde guardar:
```
web/static/js/menu.js  ← AQUÍ VA ESTE ARCHIVO
```

### Crea el archivo `menu.js`

En VS Code:
1. Click derecho en `web/static/js/`
2. "New File" → `menu.js`

### ▶️ Copia y pega:

```javascript
// Script del menú hamburguesa
document.addEventListener('DOMContentLoaded', function() {
    const hamburger = document.getElementById('hamburger');
    const navbar = document.getElementById('navbar');
    const navLinks = document.querySelectorAll('.nav-link');
    
    // Abrir/cerrar menú al hacer click en hamburguesa
    hamburger.addEventListener('click', function() {
        hamburger.classList.toggle('active');
        navbar.classList.toggle('active');
    });
    
    // Cerrar menú cuando se hace click en un enlace
    navLinks.forEach(link => {
        link.addEventListener('click', function() {
            hamburger.classList.remove('active');
            navbar.classList.remove('active');
        });
    });
    
    // Cerrar menú si se redimensiona (pasar de móvil a desktop)
    window.addEventListener('resize', function() {
        if (window.innerWidth > 768) {
            hamburger.classList.remove('active');
            navbar.classList.remove('active');
        }
    });
});
```

### ¿Qué hace?
- Cuando haces click en ☰ → Abre/cierra el menú
- Cuando haces click en un link → Cierra el menú automáticamente
- Si redimensionas la pantalla → Cierra el menú

**Guarda y continúa con PASO 12.**

---

## PASO 12: Crear la Página Home

### Tu primera página que hereda de base.html

### Crea el archivo `web/templates/home.html`

En VS Code:
1. Click derecho en `web/templates/`
2. "New File" → `home.html`

### ▶️ Copia y pega:

```html
{% extends "base.html" %}

{% block title %}Inicio - Mi Sitio Web{% endblock %}

{% block content %}
    <section class="welcome">
        <h2>{{ titulo }}</h2>
        <p class="lead">{{ mensaje }}</p>
        
        <div class="info-box">
            <h3>¿Qué es esto?</h3>
            <p>Has creado exitosamente una página web con:</p>
            <ul>
                <li>✅ <strong>Django</strong> - Framework web profesional</li>
                <li>✅ <strong>Docker</strong> - Contenedores para portabilidad</li>
                <li>✅ <strong>HTML/CSS</strong> - Diseño y estilos</li>
                <li>✅ <strong>Componentes reutilizables</strong> - Header y Footer</li>
            </ul>
        </div>

        <div class="next-steps">
            <h3>Próximos pasos:</h3>
            <ol>
                <li>Personaliza el contenido de esta página</li>
                <li>Agrega más páginas a tu sitio</li>
                <li>Crea modelos de base de datos</li>
                <li>¡Déjalo volar en internet! 🚀</li>
            </ol>
        </div>
    </section>
{% endblock %}
```

### 📚 Explicación:
- `{% extends "base.html" %}` → "Hereda la estructura de base.html" (incluyendo header y footer)
- `{{ titulo }}` y `{{ mensaje }}` → Variables que vienen de `views.py`
- Solo editas el contenido dentro de `{% block content %}...{% endblock %}`
- El header y footer se agregan automáticamente

### ¿Cómo funciona?

Cuando Django renderiza home.html:
1. Lee `{% extends "base.html" %}`
2. Carga la estructura de base.html
3. Inyecta el header desde `includes/header.html`
4. Rellena `{% block content %}` con el contenido de home.html
5. Inyecta el footer desde `includes/footer.html`
6. Devuelve el HTML completo al navegador

**Guarda y continúa con PASO 13.**

---

## PASO 13: Crear las 4 Plantillas (plantilla1, 2, 3, 4)

### Todas usan el **MISMO** código - Django rellena los datos

### 📁 Crea estos 4 archivos en `web/templates/`:
- `plantilla1.html`
- `plantilla2.html`
- `plantilla3.html`
- `plantilla4.html`

### ✨ Modelo para todas (copia y pega en CADA archivo):

```html
{% extends "base.html" %}
{% block title %}{{ titulo }} - Mi Sitio Web{% endblock %}
{% block content %}
    <section class="welcome">
        <h2>{{ titulo }}</h2>
        <p class="lead">{{ descripcion }}</p>
        <div class="info-box">
            <h3>📄 Contenido</h3>
            <p>{{ contenido }}</p>
        </div>
        <div class="info-box">
            <h3>💡 ¿Qué puedes hacer aquí?</h3>
            <ul>
                <li>✅ Personalizar el contenido</li>
                <li>✅ Agregar imágenes</li>
                <li>✅ Crear formularios</li>
                <li>✅ Conectar con base de datos</li>
            </ul>
        </div>
    </section>
{% endblock %}
```

### ¿Cómo funciona?

Cuando alguien accede a `/plantilla2/`:
1. Django ejecuta `def plantilla2(request)` (en views.py)
2. Envía datos: `{'titulo': 'Plantilla 2', 'descripcion': '...', 'contenido': '...'}`
3. Plantilla renderiza: `{{ titulo }}` → "Plantilla 2"
4. ¡Mismo HTML, datos diferentes en cada página!

**Guarda los 4 archivos y continúa con PASO 14.**

---

## PASO 14: Configurar Settings.py

### ⚠️ Django necesita saber dónde buscar templates

Django por defecto busca templates en una ruta específica dentro de cada app:
```
web/templates/web/home.html  ← Lo que Django espera por defecto
```

Pero nosotros los guardamos aquí:
```
web/templates/home.html  ← Donde los tenemos
```

**Sin esto, verás: `TemplateDoesNotExist` **

### ▶️ Edita `proyectoDjango/settings.py`

Busca `'DIRS': [],` y cámbialo a:

```python
'DIRS': [BASE_DIR / 'web' / 'templates'],
```

**Guarda el archivo y continúa con PASO 15.**

---

## PASO 15: ¡Verifica tu sitio web en el navegador!

### ¡Es hora de verlo en vivo!

Abre Terminal en tu carpeta `proyecto/` y ejecuta según tu SO:

### ▶️ Comando por Sistema Operativo

**Windows (PowerShell):**
```powershell
docker run -p 3000:3000 -v "${PWD}:/usr/src/app" -w /usr/src/app imagen_proyecto:v1.0 python manage.py runserver 0.0.0.0:3000
```

**macOS / Linux (Bash):**
```bash
docker run -p 3000:3000 -v "$(pwd):/usr/src/app" -w /usr/src/app imagen_proyecto:v1.0 python manage.py runserver 0.0.0.0:3000
```
---

Luego ve a: **http://localhost:3000/**

---

# 🐳 FASE 3 DE 3: Docker-Compose para Sistemas Profesionales Completos

## ¿Por qué FASE 3 es el cambio más importante?

### El Problema (FASE 1-2):
- ❌ Solo un contenedor
- ❌ Imposible agregar bases de datos, caché, etc.
- ❌ Difícil de llevar a producción

### La Solución (FASE 3 - Docker-Compose):
- ✅ Un comando simple: `docker-compose up`
- ✅ **MÚLTIPLES contenedores integrados**
- ✅ **Red automática entre servicios**
- ✅ Fácil escalabilidad
- ✅ **LISTO para producción profesional**

---

## 🏗️ Arquitectura Profesional: De Monolítico a Sistema Integrado

### ANTES (FASE 1-2) - Solo un contenedor:
```
┌─────────────────────────────────────┐
│     Tu PC - Desarrollo Local        │
│ ┌─────────────────────────────────┐ │
│ │   Django App (Contenedor)       │ │
│ │   Puerto 3000:3000              │ │
│ │                                 │ |
│ │   Base de datos en PC (SQLite)  | |
│ │   Peligro: Pérdida de datos     │ │
│ │                                 │ │
│ │   Sin caché (Redis)             │ │
│ └─────────────────────────────────┘ │
└─────────────────────────────────────┘
```

### DESPUÉS (FASE 3) - Sistema Profesional Integrado:
```
┌────────────────────────────────────────────────────────┐
│       Docker-Compose Network (Red Automática)          │
│                                                        │
│  ┌────────────┐   ┌─────────────┐   ┌──────────┐       │
│  │  Django    │◄─►│ PostgreSQL  │   │  Redis   │       │
│  │    App     │   │   Database  │   │  Cache   │       │
│  │ :3000      │   │   :5432     │   │  :6379   │       │
│  └────────────┘   └─────────────┘   └──────────┘       │
│        ▲                  ▲                ▲           │
│        └──────────────────┼────────────────┘           │
│                  Red DNS Automática                    │
│                                                        │
│                                                        │
│  Cada servicio puede escalar, reiniciarse, actualizarse│
│  sin afectar a los otros. Todo sincronizado.           │
└────────────────────────────────────────────────────────┘
```

---

**Todo funciona integrado automáticamente.**

### Redes Inteligentes entre Contenedores
Los contenedores se comunican entre sí automáticamente:
- Django accede a PostgreSQL: `postgresql://db:5432/...`
- Django accede a Redis: `redis://cache:6379/...`
- Nginx habla con Django: `http://web:3000`

**Sin configurar IPs, sin complicaciones. Pura magia de Docker.**

###  Desarrollo = Producción
Lo que ves en tu PC es exactamente lo que corre en el servidor:
```
Local (docker-compose up) 
    ↓
Testing  
    ↓
Producción (docker-compose.prod up)

Same config = Same results = Sin sorpresas
```

### Facilita Enorme Producción
- ✅ Funciona igual en AWS, DigitalOcean, servidor dedicado
- ✅ Bases de datos, caché, colas, todo integrado
- ✅ Logs centralizados y monitoreados
- ✅ Backups automáticos
- ✅ SSL/HTTPS fácil


---

## PASO 1: Crear el archivo `docker-compose.yml`

En tu carpeta `proyecto/`, crea un nuevo archivo llamado `docker-compose.yml` (al mismo nivel que el Dockerfile).

### Opción A: Crear archivo por Terminal (recomendado)

**Windows (PowerShell):**
```powershell
@'
version: '3.8'

services:
  web:
    build: .
    image: imagen_proyecto:v1.0
    container_name: contenedor_proyecto
    command: python manage.py runserver 0.0.0.0:3000
    volumes:
      - .:/usr/src/app
    ports:
      - "3000:3000"
    environment:
      - PYTHONUNBUFFERED=1
      - PYTHONDONTWRITEBYTECODE=1
'@ | Set-Content docker-compose.yml
```

**macOS / Linux (Bash):**
```bash
cat > docker-compose.yml << 'EOF'
version: '3.8'

services:
  web:
    build: .
    image: imagen_proyecto:v1.0
    container_name: contenedor_proyecto
    command: python manage.py runserver 0.0.0.0:3000
    volumes:
      - .:/usr/src/app
    ports:
      - "3000:3000"
    environment:
      - PYTHONUNBUFFERED=1
      - PYTHONDONTWRITEBYTECODE=1
EOF
```

### Opción B: Crear manualmente

1. Abre VS Code en tu carpeta `proyecto/`
2. Click derecho en el explorador → **"Nuevo archivo"**
3. Nómbralo: `docker-compose.yml`
4. Copia el contenido del siguiente bloque en el archivo

### ▶️ Contenido del archivo

Si usaste la **Opción A (Terminal)**, ¡ya está hecho! ✅  
Si usaste la **Opción B (VS Code)**, copia este contenido exacto:

```yaml
version: '3.8'

services:
  web:
    build: .
    image: imagen_proyecto:v1.0
    container_name: contenedor_proyecto
    command: python manage.py runserver 0.0.0.0:3000
    volumes:
      - .:/usr/src/app
    ports:
      - "3000:3000"
    environment:
      - PYTHONUNBUFFERED=1
      - PYTHONDONTWRITEBYTECODE=1
```
### Línea por línea - El YAML explicado:

| Línea | Qué significa | Por qué es importante | Escalabilidad |
|-------|---------------|----------------------|----------------|
| `version: '3.8'` | Versión de docker-compose | Compatible con Docker moderno | Soporta todas las características que necesitarás |
| `services:` | AQUÍ DEFINES TODOS TUS CONTENEDORES | Punto de crecimiento: hoy la app -web-, en el futuro podemos integrar (otra app, db, cache, nginx, backup) | Puedes tener ilimitados servicios funcionando juntos |
| `web:` | Nombre del servicio Django | Identificador único. Luego: `db:`, `cache:`, etc. | Cada servicio escala, se reinicia independientemente |
| `build: .` | Construye desde el Dockerfile en esta carpeta | Usa el Dockerfile existente que creaste | Puedes tener múltiples Dockerfiles para servicios diferentes |
| `image: imagen_proyecto:v1.0` | Nombre de la imagen con versión | Identifica la imagen exacta que se genera | Facilita versiones y reutilización |
| `container_name: contenedor_proyecto` | Nombre del contenedor | Reutilizable, facilita identificarlo con `docker ps` | Fácil debugging y monitoreo - mismo nombre en todos los comandos |
| `command:` | Comando que ejecuta al iniciar | Inicia Django automáticamente | Cada servicio ejecuta su propio comando |
| `volumes:` | Sincroniza carpetas PC ↔ contenedor | Cambios en código se ven al instante (hot-reload) | Datos persisten cuando contenedor se reinicia |
| `- .:/usr/src/app` | Tu PC ↔ /usr/src/app en contenedor | Archivos sincronizados en tiempo real | Mismo patrón para DB: PostgreSQL guarda datos en volumen |
| `ports:` | Mapeo de puertos | Acceso a app desde navegador | Django:3000, Nginx:80, PostgreSQL:5432, Redis:6379 |
| `- "3000:3000"` | Puerto 3000 local ↔ Puerto 3000 contenedor | `localhost:3000` abrirá la app | Cada servicio tiene sus propios puertos |
| `environment:` | Variables de entorno | Configuraciones, credenciales, conexiones | DATABASE_URL, REDIS_URL, claves secretas (próximo) |
| `PYTHONUNBUFFERED=1` | Logs en tiempo real sin buffer | Ves errores inmediatamente en terminal | Crítico para debugging en producción |
| `PYTHONDONTWRITEBYTECODE=1` | No crea archivos `.pyc` | Menos desorden + volumen más pequeño | Mejora rendimiento de sincronización |

✅ **Resultado:** Cada vez que ejecutes `docker-compose up`, usa la MISMA imagen y el MISMO contenedor (reutilización, menos recursos)

---

## PASO 2: Iniciar tu aplicación con Docker-Compose

### Primera vez: Ejecutar `docker-compose up`

Abre Terminal en tu carpeta `proyecto/` (donde está el `docker-compose.yml`) y ejecuta:

**Windows (PowerShell):**
```powershell
docker-compose up
```

**macOS / Linux (Bash):**
```bash
docker-compose up
```

### ¿Qué sucede automáticamente?

```
1️⃣ Docker verifica si existe la imagen: imagen_proyecto:v1.0
                    ↓
2️⃣ Si NO existe → Ejecuta automáticamente: docker build
                    ↓
3️⃣ Crea el contenedor: contenedor_proyecto
                    ↓
4️⃣ Inicia Django en http://localhost:3000
                    ↓
5️⃣ Ves los logs en directo en tu terminal
```

### ✅ Resultado esperado:

En tu terminal verás algo como:
```
[+] Running 1/1
 ✔ Container contenedor_proyecto  Created
Attaching to contenedor_proyecto
contenedor_proyecto  | Watching for file changes with StatReloader
contenedor_proyecto  | Starting development server at http://0.0.0.0:3000/
contenedor_proyecto  | Quit the server with CONTROL-C.
```

### 🌐 Abre tu navegador:

Ve a: **http://localhost:3000/**

¡Deberías ver tu sitio web funcionando!

### ⏹️ Para detener:

Presiona en la terminal: **`Ctrl + C`**

---

## Comandos utiles de `docker-compose up`

Después de la primera vez, cada vez que quieras iniciar tu app:

**Opción A: En foreground (ves los logs en terminal)**
```bash
docker-compose up
```

**Opción B: En background (liberas la terminal)**
```bash
docker-compose up -d
```

Luego, para ver los logs en cualquier momento:
```bash
docker-compose logs -f web
```

### ¿Cuándo necesitas reconstruir?

Usa `docker-compose build` SOLO si:
- ✅ Cambias `requirements.txt` (nuevos paquetes Python)
- ✅ Cambias `Dockerfile` (nueva configuración)
- ✅ Quieres forzar reconstrucción (eliminar caché)

### NO necesitas reconstruir si:
- ❌ Cambias archivos Python (views.py, models.py, etc.)
- ❌ Cambias templates HTML
- ❌ Cambias CSS o JavaScript
- ❌ Cambias archivos estáticos

### Comando para reconstruir:

```bash
docker-compose build
```

Luego inicia nuevamente:
```bash
docker-compose up
```

O en un solo comando:
```bash
docker-compose up --build
```

---

### Los comandos más comunes:

| Comando | Qué hace | Ejemplo |
|---------|----------|---------|
| `docker-compose up` | Inicia todos los servicios (ver logs) | `docker-compose up` |
| `docker-compose up -d` | Inicia en background (sin logs) | `docker-compose up -d` |
| `docker-compose down` | Detiene y elimina contenedores | `docker-compose down` |
| `docker-compose logs -f web` | Ve logs en tiempo real | `docker-compose logs -f web` |
| `docker-compose build` | Reconstruye imagen | `docker-compose build` |
| `docker-compose exec web bash` | Accede a terminal del contenedor | `docker-compose exec web bash` |
| `docker-compose ps` | Ver estado de servicios | `docker-compose ps` |
| `docker-compose restart` | Reinicia todos los servicios | `docker-compose restart` |

---

## ✨ Lo que Aprendiste en FASE 3

### Conceptos Clave:
✅ Docker-Compose es el estándar profesional para Django  
✅ UN archivo YAML define TODO tu sistema  
✅ Múltiples servicios se comunican automáticamente  
✅ Volúmenes permiten desarrollo rápido (hot-reload)  
✅ Mismo archivo en desarrollo, testing y producción  
✅ Escalable desde lo simple a lo complejo  

### Habilidades Adquiridas:
✅ Crear y entender `docker-compose.yml`  
✅ Ejecutar múltiples contenedores coordinados  
✅ Usar redes automáticas de Docker  
✅ Persistencia de datos con volúmenes  
✅ Variables de entorno para configuración  
✅ Preparación para producción  

---

## 🚀 Próximos Pasos:

### Nivel Intermedio (Con Docker-Compose):
- ✅ Agregar PostgreSQL como base de datos 
- ✅ Agregar Redis para caché y sesiones
- ✅ Configurar Nginx como reverse proxy
- ✅ Agregar SSL/HTTPS automático
- ✅ Sistema de respaldos automáticos

### Nivel Avanzado (Aplicación Completa):
- ✅ Agregar formularios de contacto
- ✅ Sistema de usuarios y autenticación
- ✅ Panel de administración profesional
- ✅ API REST con Django REST Framework
- ✅ Sistema de notificaciones por email

### Producción (Escala Profesional):
- ✅ Cambiar a gunicorn (servidor profesional, no dev)
- ✅ Archivo `.env` para credenciales secretas
- ✅ CI/CD con GitHub Actions
- ✅ Monitoreo automático de errores
- ✅ Copias de seguridad automáticas diarias
- ✅ Desplegar a AWS, DigitalOcean, Heroku, Azure
- ✅ Certificados SSL automáticos con Let's Encrypt

---
## 📚 Glosario Completo - Términos Clave 

| Término | Significado | En tu proyecto |
|---------|-----------|-----------------|
| **HTML** | Lenguaje para crear estructuras de páginas web | templates/base.html |
| **CSS** | Lenguaje para hacer que las páginas se vean bonitas | static/css/style.css |
| **JavaScript** | Lenguaje para hacer que las páginas sean interactivas | static/js/menu.js |
| **Django** | Framework (herramienta) Python para crear sitios web profesionales | proyectoDjango/ |
| **Docker** | Contenedor - empaqueta tu aplicación para que funcione en cualquier PC | Dockerfile |
| **Imagen** | Plantilla/Receta de Docker (como un .ISO) | `imagen_proyecto:v1.0` |
| **Contenedor** | Instancia ejecutando la imagen (como una máquina virtual activa) | `contenedor_proyecto` |
| **Tag/Etiqueta** | Versión o variante de una imagen | `v1.0` en `imagen_proyecto:v1.0` |
| **Dockerfile** | Archivo que define cómo construir la imagen | FASE 1, PASO 3 |
| **Docker-Compose** | Herramienta para definir y ejecutar múltiples contenedores con un archivo YAML | docker-compose.yml |
| **YAML** | Formato de archivo legible para humanos (usa espacios y colones, no llaves) | docker-compose.yml |
| **Build** | Compilar Dockerfile para crear una imagen | `docker build` / `docker-compose build` |
| **Service** | Servicio individual en docker-compose (en tu caso: "web") | services: web: |
| **Template** | Archivo HTML que Django rellena con datos (dinámico) | templates/home.html |
| **View** | Función Python que procesa datos y devuelve un template | web/views.py |
| **URL** | Dirección web (http://localhost:3000/) | web/urls.py |
| **Navbar** | Barra de navegación (menú) | templates/header.html |
| **Responsive** | Que se adapta a móviles, tablets, desktops | CSS con media queries |
| **Hot-Reload** | Cambios en código se ven automáticamente sin reiniciar | Volumen + PYTHONUNBUFFERED=1 |
| **Volumen** | Sincronización de carpetas entre PC y contenedor Docker | `.:/usr/src/app` en docker-compose.yml |
| **Port Mapping** | Conexión puerto PC ↔ puerto contenedor | `-p 3000:3000` |
| **Environment Variables** | Configuraciones que se pasan al contenedor | `PYTHONUNBUFFERED=1` |
| **Versioning** | Control de versiones de la imagen | `v1.0`, `v2.0`, etc. |

---

## 🎓 ¿Quieres aprender más?

- [Django Oficial](https://www.djangoproject.com/)
- [MDN Web Docs (HTML/CSS/JS)](https://developer.mozilla.org/)
- [Docker Oficial](https://www.docker.com/)

---
