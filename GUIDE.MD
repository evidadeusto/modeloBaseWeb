# GUIDE: Creating a Professional Website

## What will you learn?

This guide teaches you how to create a professional website using **Django** (a Python framework) and **Docker** (containers).

> **NOTE:** You don't need previous programming experience.

**This guide includes 3 phases, in which you will learn:**
1. **PHASE 1** → Configure the basic environment (Django + Docker)
2. **PHASE 2** → Create your first functional web page
3. **PHASE 3** → Create a simplified process using docker-compose.

### Software Requirements

Before you start, make sure you have:

- **Operating System:** Windows, macOS or Linux
- **[Docker Desktop installed](https://www.docker.com/products/docker-desktop).** Download and install. (Special case for macOS, you will receive a request to install Rosetta 2 automatically, which is necessary.)
- **[Visual Studio Code installed](https://code.visualstudio.com/download)** (code editor)


### 📑 Quick Index - Navigate All Phases
- [PHASE 1: Basic Project Structure](#phase-1-of-3-basic-project-structure)
- [PHASE 2: Functional Web Page](#phase-2-of-3-create-your-functional-web-page)
- [PHASE 3: Docker-Compose](#phase-3-of-3-docker-compose-for-complete-professional-systems)
- [Glossary: Key Terms](#complete-glossary---key-terms) 

---

## PHASE 1 OF 3: Basic Project Structure

# 📁 PHASE 1 OF 3: Basic Project Structure

## STEP 0: Prior Preparation

### ✅ Step A: Verify that Docker is installed

Open a terminal/PowerShell and run:

```bash
docker --version
docker-compose --version
```

**You should see something like:**
```
Docker version 24.0.0
Docker Compose version v2.20.0
```

If they don't appear, download and install [Docker Desktop](https://www.docker.com/products/docker-desktop) first.

---

### (OPTIONAL) Validate Docker with your first container

To make sure everything works correctly, run this test command:

```bash
docker run hello-world
```

**What will happen?**
- Docker will download a small test image
- Create a container and run it
- Display a welcome message

**You will see this in the terminal:**
```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

**Why is it useful?** 
✅ Validates that Docker works without problems  
✅ Tests internet connection (downloads the image)  
✅ Caches the image for future tests (faster)  
✅ Gives you confidence that everything is ready  

> **Note:** This step is optional but **RECOMMENDED**. If you don't want to do it, skip directly to Step B.

---

### ✅ Step B: Create project folder

**On Windows:**
1. Open File Explorer
2. Go to where you want your project (e.g., `Documents`)
3. Right-click → New Folder → Name it `project`
4. Right-click on `project` → "Open in Terminal" or "Open PowerShell here"

**On Mac:**
1. Open Finder
2. Go to Documents (or your preferred folder)
3. Right-click → New Folder → Name it `project`
4. Open Terminal (Applications → Utilities → Terminal)
5. Type: `cd ~/Documents/project` (adjust the path if different)

**On Linux:**
1. Open file manager (Nautilus, Dolphin, etc.)
2. Go to your preferred folder (e.g., Documents)
3. Right-click → Create Folder → Name it `project`
4. Right-click on `project` → "Open Terminal Here"
5. Or open terminal and type: `cd ~/Documents/project` (adjust as needed)

---

### ✅ Step C: Open the folder in Visual Studio Code

1. Open Visual Studio Code
2. Click "File" → "Open Folder"
3. Select the `project` folder you created
4. Click "Select Folder"

**Do you see the folder on the left side?** ✅ **Perfect! Continue with STEP 1.**

---

## STEP 1: Create Django Project with Docker

### What will happen?

We will tell Docker to execute a command inside a container. Django is a framework (tool) that makes it easier to create websites.

### ▶️ Command to run

**Select your Operating System:**

**Windows (PowerShell):**
```powershell
docker run --rm -v "${PWD}:/usr/src/app" -w /usr/src/app python:3.11-slim sh -c "pip install django && django-admin startproject djangoProject ."
```

**macOS / Linux (Bash):**
```bash
docker run --rm -v "$(pwd):/usr/src/app" -w /usr/src/app python:3.11-slim sh -c "pip install django && django-admin startproject djangoProject ."
```

> **Note about PWD:** `${PWD}` in PowerShell vs `$(pwd)` in Bash. Both mean "current folder". Django creates the same files.

### What does each part of the command do?
| Component | What it does |
|-----------|----------|
| `docker run` | Runs a container |
| `--rm` | Removes it when finished |
| `-v "${PWD}:/usr/src/app"` | Mounts your current folder inside the container |
| `-w /usr/src/app` | Works inside that directory |
| `python:3.11-slim` | Python 3.11 image (lightweight) |
| `pip install django` | Installs Django |
| `django-admin startproject djangoProject .` | Creates the project called djangoProject |

And this structure is automatically created in your folder:
```
project/
├── manage.py
├── djangoProject/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
```

---

## STEP 2: Create requirements.txt 

### 📝 What is requirements.txt?

It's a file that lists **all the tools (packages) your project needs**. These are the basic requirements so others can reproduce your project.

### ▶️ Option 1: Terminal (recommended)

**Windows (PowerShell):**
```powershell
echo Django==5.0 > requirements.txt
```

**macOS / Linux (Bash):**
```bash
echo "Django==5.0" > requirements.txt
```

### Option 2: Text Editor

1. Create a file called `requirements.txt`
2. Write this inside:
```
Django==5.0
```
3. Save the file

### ✅ Verify it exists in your folder and continue with STEP 3.

---

## STEP 3: Create Dockerfile

### 🐳 What is Dockerfile?

**Dockerfile** is a file of "instructions" that tells Docker how to build your container. It's like a blueprint for building a house.

### ▶️ Option 1: Terminal (recommended)

**Windows (PowerShell)** - Copy the entire block:
```powershell
@'
FROM python:3.11-slim

# Prevents bytecode and forces real-time log output
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Compilation tools for libraries that need them
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

**macOS / Linux (Bash)** - Copy the entire block:
```bash
cat << 'EOF' > Dockerfile
FROM python:3.11-slim

# Prevents bytecode and forces real-time log output
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Compilation tools for libraries that need them
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

### Option 2: Text Editor

1. Create a file called `Dockerfile` (no extension)
2. Copy and paste this content:

```dockerfile
FROM python:3.11-slim

# Prevents bytecode and forces real-time log output
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Compilation tools for libraries that need them
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

3. Save the file as `Dockerfile`

### 📚 Line-by-line explanation
| Line | What it does |
|-------|----------|
| `FROM python:3.11-slim` | Uses Python 3.11 image (small) |
| `ENV PYTHONDONTWRITEBYTECODE=1` | Prevents generating `.pyc` files (compiled bytecode) - reduces size |
| `ENV PYTHONUNBUFFERED=1` | Forces real-time logs without buffer - better debugging in Docker |
| `RUN apt-get update...` | Installs compilation tools (gcc, build-essential) needed for complex Python libraries |
| `rm -rf /var/lib/apt/lists/*` | Cleans apt cache after installing - reduces image by ~100MB |
| `WORKDIR /usr/src/app` | Creates work directory **following professional Unix convention.**  |
| `COPY requirements.txt .` | Copies requirements.txt to the container |
| `RUN pip install --no-cache-dir --upgrade pip` | Upgrades pip and avoids caching dependencies - reduces image by ~50-100MB |
| `RUN pip install --no-cache-dir -r requirements.txt` | Installs dependencies without caching |
| `COPY . .` | Copies all project code |
| `EXPOSE 3000` | Opens port 3000 |
| `CMD ["python", "manage.py", "runserver", "0.0.0.0:3000"]` | Command that runs when container starts |

---

## STEP 4: Build the image

### Compile the Dockerfile

Run this command:

```bash
docker build -t image_project:v1.0 .
```

### 📚 Command breakdown

| Part | What it means |
|-------|---------------|
| `docker build` | Automatically compiles the Dockerfile |
| `-t` | Assigns a name and tag to the image |
| `image_project` | **Name** of the image (main identifier) |
| `v1.0` | **Tag** of the image (version or variant) |
| `.` | Looks for Dockerfile in current folder |

### What's the difference between name and tag?

```
image_project:v1.0

name ↓          ↓ tag
  
Name = Unique identifier of the image
Tag = Version or variant of that image

Example with versions:
- project_container:v1.0
- project_container:v2.0
- project_container:production
- project_container:development
```

### ✅ Benefits of using names and tags

- ✅ You can have multiple versions of the same image
- ✅ Quickly identify which version you use
- ✅ Useful for switching between development and production
- ✅ Facilitates change control

### How long does it take?

**First time:** ~2-3 minutes (downloads dependencies)  
**Next times:** Faster (uses cache)

## STEP 5: Verify the image was created 

### ✅ Confirmation

Run this command to see your images:

```bash
docker images
```

You should see `project_container` with tag `website` in the list. If you didn't create images before, it will be the only one in the list.

---

## STEP 6: Run migrations - Create database 

### What are migrations?

**Migrations** are organized database changes. It's like a "change history" that Django controls automatically.

### ▶️ Command

**Windows (PowerShell):**
```powershell
docker run --rm -v "${PWD}:/usr/src/app" -w /usr/src/app image_project:v1.0 python manage.py migrate
```

**macOS / Linux (Bash):**
```bash
docker run --rm -v "$(pwd):/usr/src/app" -w /usr/src/app image_project:v1.0 python manage.py migrate
```


### Command explanation
| Component | What it does |
|-----------|----------|
| `docker run` | Runs a container |
| `--rm` | Removes the container when finished |
| `-v "${PWD}:/usr/src/app"` | Syncs your current folder with `/usr/src/app` in container |
| `-w /usr/src/app` | Sets the work directory |
| `image_project:v1.0` | Uses the image you created |
| `python manage.py migrate` | Runs Django migrations |

### What result do you get?
- ✅ Creates the SQLite database (`db.sqlite3`)
- ✅ Generates all tables needed for Django
- ✅ **Without this, the admin won't work**

---

## STEP 7: Create superuser - Administrator 

### What is a superuser?

A **superuser** is an administrator user with full permissions. You'll use this to access Django's admin panel.

### ▶️ Command (will be interactive)

**Windows (PowerShell):**
```powershell
docker run --rm -it -v "${PWD}:/usr/src/app" -w /usr/src/app image_project:v1.0 python manage.py createsuperuser
```

**macOS / Linux (Bash):**
```bash
docker run --rm -it -v "$(pwd):/usr/src/app" -w /usr/src/app image_project:v1.0 python manage.py createsuperuser
```

### Command explanation
| Component | What it does |
|-----------|----------|
| `docker run` | Runs a container |
| `--rm` | Removes the container when finished |
| `-i` | Interactive mode (stdin input) |
| `-t` | Assigns pseudo-terminal |
| `-v "${PWD}:/usr/src/app"` | Syncs current folder with `/usr/src/app` |
| `-w /usr/src/app` | Sets work directory |
| `image_project:v1.0` | Uses the created image |
| `python manage.py createsuperuser` | Creates an administrator user |

### What result do you get?
- ✅ Asks you for: username, email and password
- ✅ Creates the administrator user
- ⚠️ **Keep this data safe** - you'll use it to access the admin panel.

---

## STEP 8: Start server - Go online 
### What will happen?

Your website will be available at `http://localhost:3000` (only on your PC locally).

> **NOTE:** These commands are long because they include all options (`-v`, `-w`, `-p`). In **PHASE 3** you'll learn to simplify them with `docker-compose.yml`. For now, understand each parameter to learn how Docker really works. 

### ▶️ Command

**Windows (PowerShell):**
```powershell
docker run -p 3000:3000 -v "${PWD}:/usr/src/app" -w /usr/src/app image_project:v1.0 python manage.py runserver 0.0.0.0:3000
```

**macOS / Linux (Bash):**
```bash
docker run -p 3000:3000 -v "$(pwd):/usr/src/app" -w /usr/src/app image_project:v1.0 python manage.py runserver 0.0.0.0:3000
```

### Command explanation
| Component | What it does |
|-----------|----------|
| `docker run` | Runs a container |
| `-p 3000:3000` | Maps port 3000 PC → port 3000 container |
| `-v "${PWD}:/usr/src/app"` | Syncs your current folder with `/usr/src/app` |
| `-w /usr/src/app` | Sets work directory |
| `image_project:v1.0` | Uses the created image |
| `python manage.py runserver` | Starts the Django server |
| `0.0.0.0:3000` | Listens on all interfaces on port 3000 |

### What result do you get?
- ✅ Django runs at **http://localhost:3000**
- ✅ File changes are automatically detected
- ⏹️ To stop: press `Ctrl + C`

---

## STEP 9: Access the administration panel

### 🎛️ What is the admin panel?

It's an interface where you can manage your website without writing code. It comes included with Django automatically.

### ▶️ Steps

In your browser go to:
```
http://localhost:3000/admin/
```

Log in with:
- **Username:** (the one you created in STEP 7)
- **Password:** (the one you created in STEP 7)

✅ **Admin panel ready to use!**

---

## ✅ Final status - PHASE 1 completed

After completing all 9 steps, your folder should look like this:

```
project/
├── manage.py                  ← ✅ STEP 1
├── requirements.txt           ← ✅ STEP 2
├── Dockerfile                 ← ✅ STEP 3
├── db.sqlite3                 ← ✅ STEP 6 (database)
└── djangoProject/
    ├── settings.py           ← ✅ STEP 1
    ├── urls.py               ← ✅ STEP 1
    ├── asgi.py               ← ✅ STEP 1
    ├── wsgi.py               ← ✅ STEP 1
    └── __init__.py           ← Internal configuration
```

---

## PHASE 2 OF 3: Create Your Functional Web Page

# 📁 PHASE 2 OF 3: Create Your Functional Web Page

> **In this phase:** We will build your first **completely functional** website with navbar, multiple pages and professional styles.

### What we will create:

```
Your final website will look like this:

┌─────────────────────────────────────┐
│ My Website                          │  ← Header
│ HOME | TEMPLATE 1 | TEMPLATE 2...   │
├─────────────────────────────────────┤
│                                     │
│  Content of the current page        │  ← Main
│                                     │
├─────────────────────────────────────┤
│ © 2026 My Website                   │  ← Footer
└─────────────────────────────────────┘

```

### 15 simple steps:

1. **STEPS 1-6:** Prepare the app (create, register, folders, routes, views)
2. **STEPS 7-11:** Create components (header, footer, base, CSS, JavaScript)
3. **STEPS 12-13:** Create pages (home + 4 templates)
4. **STEP 14:** Configure Django (settings.py)
5. **STEP 15:** View in browser and test

## STEP 1: Create the `web` app

### What is an "app" in Django?

An **app** is like a component or module inside your project. It's simply a way to organize your code by topic within the same program. Where you'll store:
- ✅ Your web pages (HTML templates)
- ✅ The logic that processes data (views)
- ✅ Visual designs (CSS)
- ✅ Images and files

You can have several apps in a project. In our case, we'll create a main app called `web/`.

### ▶️ Command to create the app

**Windows (PowerShell):**
```powershell
docker run --rm -v "${PWD}:/usr/src/app" -w /usr/src/app image_project:v1.0 python manage.py startapp web
```

**macOS/Linux (Bash):**
```bash
docker run --rm -v "$(pwd):/usr/src/app" -w /usr/src/app image_project:v1.0 python manage.py startapp web
```

### What does Django create?

This folder will be automatically generated:

```
web/
├── migrations/          ← Database change history
│   └── __init__.py
├── __init__.py
├── admin.py            ← Register models in admin panel
├── apps.py             ← App configuration
├── models.py           ← Data structure (DB tables)
├── tests.py            ← Automatic tests
└── views.py            ← Your website logic ⭐
```

**Perfect! Continue with STEP 2.**

---

## STEP 2: Register the app in Django

### Why is it necessary?

Django needs to "know" all your apps. If you don't register it, Django ignores it completely.

### ▶️ Edit the file `djangoProject/settings.py`

1. Open the file in VS Code
2. Find the section called `INSTALLED_APPS` (around line 33)
3. It should look like this:

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

4. **Add `'web',` at the end (before the last bracket):**

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'web',  ← ✅ ADD THIS LINE
]
```

5. **Save the file** (Ctrl+S or Cmd+S)

✅ **Done! Continue with STEP 3.**

---

## STEP 3: Create folders for templates and static files

### 📁 What are we going to create?

Your website needs a well-organized folder structure:

**templates/** → HTML files (the pages)
- `base.html` → Base template (common structure)
- `home.html` → Home page
- `includes/` → Reusable components

**static/** → Styles, scripts and images
- `css/` → CSS styles
- `js/` → JavaScript scripts
- `img/` → Images
- And other resources...

### 📚 Why this structure?

**DRY** (Don't Repeat Yourself) → Don't repeat code
- ✅ Header and footer in 1 file (`includes/`) 
- ✅ Used on all pages with `{% include %}`
- ✅ If you change the design, change in 1 place

### ▶️ On Windows (PowerShell)

Copy and paste these commands one by one:

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

### ▶️ On macOS/Linux

Open Terminal in your project folder and run:

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

> **Note:** The `-p` parameter on macOS/Linux creates all nested directories at once.

### ✅ Verification

In VS Code, you should see the structure like this in the left panel:

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
└── (other files...)
```

✅ **Continue with STEP 4.**

---

## STEP 4: Create the routes file `web/urls.py`

### 🔗 What is a routes file?

It's like an "address map" of your website. It defines what page is displayed when someone accesses each URL.

### ▶️ Option 1: Create with terminal (recommended)

**On Windows (PowerShell):**
```powershell
New-Item web\urls.py -ItemType File
```

**On macOS/Linux:**
```bash
touch web/urls.py
```

### Option 2: Create manually in VS Code

1. Right-click on the `web/` folder
2. "New File" → type `urls.py`

### ▶️ Now add this content

Open `web/urls.py` and copy-paste this:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
    path('template1/', views.template1, name='template1'),
    path('template2/', views.template2, name='template2'),
    path('template3/', views.template3, name='template3'),
    path('template4/', views.template4, name='template4'),
]
```

### 📚 Explanation:
- `path('', ...)` → Root URL (http://localhost:3000/)
- `path('template1/', ...)` → URL for template 1 (http://localhost:3000/template1/)
- `path('template2/', ...)` → URL for template 2 (http://localhost:3000/template2/)
- And so on with the others...

### **Important:**
- `name='template1'` → This name is used in the header with `{% url 'template1' %}`
- Must match exactly with the functions in `views.py`

**Save the file and continue with STEP 5.**

---

## STEP 5: Connect the routes to the project

### Why?

This way Django knows it should use the routes from your `web` app.

### ▶️ Edit `djangoProject/urls.py`

1. Open the file `djangoProject/urls.py`
2. Find the current content (should look like this):

```python
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

3. **Modify to this:**

```python
from django.contrib import admin
from django.urls import path, include  ← ADD: ", include"

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('web.urls')),  ← ADD THIS NEW LINE
]
```

### 📚 Explanation:
- `include('web.urls')` → "Import all routes from the `web/urls.py` file"
- `path('', ...)` → "Use those routes at the root of the site"

**Save the file and continue with STEP 6.**

---

## STEP 6: Create the Views in `web/views.py`

### What is a view?

A **view** is a Python function that:
1. **Receives** a request from the browser
2. **Processes** data
3. **Returns** an HTML page with data

### 📁 File where to save:
```
web/views.py  ← EVERYTHING GOES HERE
```

### ▶️ Replace ALL the content of `web/views.py` with this:

```python
from django.shortcuts import render

def home(request):
    """Home page view"""
    context = {
        'title': 'Welcome to your website!',
        'message': 'This is your first page created with Django and Docker',
    }
    return render(request, 'home.html', context)

def template1(request):
    """Template 1 view"""
    context = {
        'title': 'Template 1',
        'description': 'First example page',
        'content': 'You can add your content here...',
    }
    return render(request, 'template1.html', context)

def template2(request):
    """Template 2 view"""
    context = {
        'title': 'Template 2',
        'description': 'Second example page',
        'content': 'You can add your content here...',
    }
    return render(request, 'template2.html', context)

def template3(request):
    """Template 3 view"""
    context = {
        'title': 'Template 3',
        'description': 'Third example page',
        'content': 'You can add your content here...',
    }
    return render(request, 'template3.html', context)

def template4(request):
    """Template 4 view"""
    context = {
        'title': 'Template 4',
        'description': 'Fourth example page',
        'content': 'You can add your content here...',
    }
    return render(request, 'template4.html', context)
```

### 📝 Simple explanation:

Each function:
- ✅ Receives a request (`request`)
- ✅ Creates a `context` dictionary with data
- ✅ Returns the rendered HTML with `render()`

**In HTML you'll access the data with:**
- `{{ title }}`
- `{{ description }}`
- `{{ content }}`

### 🎯 What is `context`?

It's the "bridge" between Python (backend) and HTML (frontend):

```
Python (views.py)           HTML (templates)
context = {
    'title': '...'    →    {{ title }}
    'message': '...'   →    {{ message }}
}
```

**Save the file and continue with STEP 7.**

---

## STEP 7: Create the Header with Professional Navbar

### What are we going to do?

We'll create a header with:
- 📌 Title and subtitle centered
- 🔗 Navigation menu with links
- 📱 Hamburger menu (appears on mobile)

### 📁 Folder where to save:
```
web/templates/includes/header.html  ← THIS FILE GOES HERE
```

### ▶️ Create the `header.html` file

In VS Code:
1. Right-click on the `web/templates/includes/` folder
2. "New File" → `header.html`

### ▶️ Copy and paste this code:

```html
<!-- Header Component - Header component with navbar -->
<header class="header">
    <!-- Title and subtitle section (centered) -->
    <div class="header-intro">
        <div class="container">
            <h1>🚀 My Website</h1>
            <p class="subtitle">Created with Django and Docker</p>
        </div>
    </div>
    
    <!-- Navigation Section -->
    <div class="header-navbar">
        <div class="container navbar-container">
            <!-- Hamburger Menu (only visible on mobile) -->
            <button class="hamburger" id="hamburger" aria-label="Menu">
                <span></span>
                <span></span>
                <span></span>
            </button>
            
            <!-- Navigation Menu -->
            <nav class="navbar" id="navbar">
                <ul class="nav-menu">
                    <li><a href="{% url 'home' %}" class="nav-link">HOME</a></li>
                    <li><a href="{% url 'template1' %}" class="nav-link">TEMPLATE 1</a></li>
                    <li><a href="{% url 'template2' %}" class="nav-link">TEMPLATE 2</a></li>
                    <li><a href="{% url 'template3' %}" class="nav-link">TEMPLATE 3</a></li>
                    <li><a href="{% url 'template4' %}" class="nav-link">TEMPLATE 4</a></li>
                </ul>
            </nav>
        </div>
    </div>
</header>
```

### 🔍 What does each part do?

| Element | Function |
|----------|---------|
| `header-intro` | Title + Subtitle in the center |
| `header-navbar` | Menu container |
| `hamburger` | ☰ button (only appears on mobile) |
| `navbar` | Horizontal navigation menu |
| `nav-menu` | List of links (HOME, TEMPLATE 1, etc) |

### 📝 IMPORTANT:
- `{% url 'home' %}` → Generates link to home page
- `{% url 'template1' %}` → Generates link to template 1
- These links will work when we create the routes in `urls.py`

**Save the file and continue with STEP 8.**

---

## STEP 8: Create the Footer

### Folder where to save:
```
web/templates/includes/footer.html  ← THIS FILE GOES HERE
```

### ▶️ Create the `footer.html` file

In VS Code:
1. Right-click on `web/templates/includes/`
2. "New File" → `footer.html`

### ▶️ Copy and paste:

```html
<!-- Footer Component - Footer component -->
<footer class="footer">
    <p>&copy; 2026 My Website. All rights reserved.</p>
    <p><small>Created with ❤️ using Django and Docker</small></p>
</footer>
```

**Save and continue with STEP 9.**

---

## STEP 9: Create the Base Template `base.html`

### The structure used by your entire page

### Folder where to save:
```
web/templates/base.html  ← THIS FILE GOES HERE
```

### ▶️ Create the `base.html` file

### ▶️ Copy and paste:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}My Website{% endblock %}</title>
    {% load static %}
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
    <!-- Include header component -->
    {% include "includes/header.html" %}

    <!-- Specific content of each page -->
    <main class="container">
        {% block content %}
        <!-- Here goes the specific content of each page -->
        {% endblock %}
    </main>

    <!-- Include footer component -->
    {% include "includes/footer.html" %}
    
    <!-- Hamburger menu script -->
    {% load static %}
    <script src="{% static 'js/menu.js' %}"></script>
</body>
</html>
```

### 📝 Important:
- `{% include %}` → Injects header.html and footer.html here
- `{% block content %}` → Each page fills this section
- `<script src="{% static 'js/menu.js' %}">` → Adds interactivity to the menu

**Save and continue with STEP 10.**

---

## STEP 10: Create the CSS Styles for Navbar and Site

### Here we do the visual design.

### 📁 Folder where to save:
```
web/static/css/style.css  ← THIS FILE GOES HERE
```

### Create the `style.css` file

In VS Code:
1. Right-click on `web/static/css/`
2. "New File" → `style.css`

### ▶️ Copy and paste ALL this CSS:

<details>
<summary>✨ Click to view/copy complete CSS</summary>

```css
/* ==================== RESET AND GENERALS ==================== */
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

/* ==================== HAMBURGER ==================== */
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

/* ==================== RESPONSIVE - SMALL MOBILE (480px) ==================== */
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

### What this CSS does:
- ✅ Nice style for the header (purple gradient)
- ✅ Horizontal navbar on desktop
- ✅ Hamburger visible on mobile
- ✅ Smooth animations (hover, transitions)
- ✅ Responsive on tablet and mobile

**Save and continue with STEP 11.**

---

## STEP 11: Create the Hamburger Menu JavaScript

### Now let's make the menu interactive

### Folder where to save:
```
web/static/js/menu.js  ← THIS FILE GOES HERE
```

### Create the `menu.js` file

In VS Code:
1. Right-click on `web/static/js/`
2. "New File" → `menu.js`

### ▶️ Copy and paste:

```javascript
// Hamburger menu script
document.addEventListener('DOMContentLoaded', function() {
    const hamburger = document.getElementById('hamburger');
    const navbar = document.getElementById('navbar');
    const navLinks = document.querySelectorAll('.nav-link');
    
    // Open/close menu when clicking hamburger
    hamburger.addEventListener('click', function() {
        hamburger.classList.toggle('active');
        navbar.classList.toggle('active');
    });
    
    // Close menu when clicking a link
    navLinks.forEach(link => {
        link.addEventListener('click', function() {
            hamburger.classList.remove('active');
            navbar.classList.remove('active');
        });
    });
    
    // Close menu if you resize (switching from mobile to desktop)
    window.addEventListener('resize', function() {
        if (window.innerWidth > 768) {
            hamburger.classList.remove('active');
            navbar.classList.remove('active');
        }
    });
});
```

### What does it do?
- When you click ☰ → Opens/closes the menu
- When you click a link → Automatically closes the menu
- If you resize the screen → Closes the menu

**Save and continue with STEP 12.**

---

## STEP 12: Create the Home Page

### Your first page that inherits from base.html

### Create the file `web/templates/home.html`

In VS Code:
1. Right-click on `web/templates/`
2. "New File" → `home.html`

### ▶️ Copy and paste:

```html
{% extends "base.html" %}

{% block title %}Home - My Website{% endblock %}

{% block content %}
    <section class="welcome">
        <h2>{{ title }}</h2>
        <p class="lead">{{ message }}</p>
        
        <div class="info-box">
            <h3>What is this?</h3>
            <p>You have successfully created a website with:</p>
            <ul>
                <li>✅ <strong>Django</strong> - Professional web framework</li>
                <li>✅ <strong>Docker</strong> - Containers for portability</li>
                <li>✅ <strong>HTML/CSS</strong> - Design and styles</li>
                <li>✅ <strong>Reusable components</strong> - Header and Footer</li>
            </ul>
        </div>

        <div class="next-steps">
            <h3>Next steps:</h3>
            <ol>
                <li>Customize the content of this page</li>
                <li>Add more pages to your site</li>
                <li>Create database models</li>
                <li>Let it fly on the internet! 🚀</li>
            </ol>
        </div>
    </section>
{% endblock %}
```

### 📚 Explanation:
- `{% extends "base.html" %}` → "Inherits the structure from base.html" (including header and footer)
- `{{ title }}` and `{{ message }}` → Variables coming from `views.py`
- Only edit the content inside `{% block content %}...{% endblock %}`
- Header and footer are added automatically

### How does it work?

When Django renders home.html:
1. Reads `{% extends "base.html" %}`
2. Loads base.html structure
3. Injects header from `includes/header.html`
4. Fills `{% block content %}` with home.html content
5. Injects footer from `includes/footer.html`
6. Returns the complete HTML to the browser

**Save and continue with STEP 13.**

---

## STEP 13: Create the 4 Templates (template1, 2, 3, 4)

### All use the **SAME** code - Django fills the data

### 📁 Create these 4 files in `web/templates/`:
- `template1.html`
- `template2.html`
- `template3.html`
- `template4.html`

### ✨ Template for all (copy and paste in EACH file):

```html
{% extends "base.html" %}
{% block title %}{{ title }} - My Website{% endblock %}
{% block content %}
    <section class="welcome">
        <h2>{{ title }}</h2>
        <p class="lead">{{ description }}</p>
        <div class="info-box">
            <h3>📄 Content</h3>
            <p>{{ content }}</p>
        </div>
        <div class="info-box">
            <h3>💡 What can you do here?</h3>
            <ul>
                <li>✅ Customize the content</li>
                <li>✅ Add images</li>
                <li>✅ Create forms</li>
                <li>✅ Connect to database</li>
            </ul>
        </div>
    </section>
{% endblock %}
```

### How does it work?

When someone accesses `/template2/`:
1. Django runs `def template2(request)` (in views.py)
2. Sends data: `{'titulo': 'Template 2', 'descripcion': '...', 'contenido': '...'}`
3. Template renders: `{{ titulo }}` → "Template 2"
4. Same HTML, different data on each page!

**Save all 4 files and continue with STEP 14.**

---

## STEP 14: Configure Settings.py

### ⚠️ Django needs to know where to look for templates

Django by default looks for templates in a specific path inside each app:
```
web/templates/web/home.html  ← What Django expects by default
```

But we saved them here:
```
web/templates/home.html  ← Where we have them
```

**Without this, you'll see: `TemplateDoesNotExist` **

### ▶️ Edit `djangoProject/settings.py`

Find `'DIRS': [],` and change it to:

```python
'DIRS': [BASE_DIR / 'web' / 'templates'],
```

**Save the file and continue with STEP 15.**

---

## STEP 15: Verify your website in the browser!

### It's time to see it live!

Open Terminal in your `project/` folder and run according to your OS:

### ▶️ Command by Operating System

**Windows (PowerShell):**
```powershell
docker run -p 3000:3000 -v "${PWD}:/usr/src/app" -w /usr/src/app image_project:v1.0 python manage.py runserver 0.0.0.0:3000
```

**macOS / Linux (Bash):**
```bash
docker run -p 3000:3000 -v "$(pwd):/usr/src/app" -w /usr/src/app image_project:v1.0 python manage.py runserver 0.0.0.0:3000
```

**Open your browser and go to:** `http://localhost:3000`

---

## PHASE 3 OF 3: Docker-Compose for Complete Professional Systems

# 🐳 PHASE 3 OF 3: Docker-Compose for Complete Professional Systems

## Why is PHASE 3 the Most Important Change?

### The Problem (PHASE 1-2):
- ❌ Only one container
- ❌ Impossible to add databases, cache, etc.
- ❌ Difficult to take to production

### The Solution (PHASE 3 - Docker-Compose):
- ✅ One simple command: `docker-compose up`
- ✅ **MULTIPLE integrated containers**
- ✅ **Automatic network between services**
- ✅ Easy scalability
- ✅ **READY for professional production**

---

## 🏗️ Professional Architecture: From Monolithic to Integrated System

### BEFORE (PHASE 1-2) - Only one container:
```
┌─────────────────────────────────────┐
│     Your PC - Local Development     │
│ ┌─────────────────────────────────┐ │
│ │   Django App (Container)        │ │
│ │   Port 3000:3000                │ │
│ │                                 │ |
│ │   Database on PC (SQLite)       | |
│ │   Danger: Data Loss             │ │
│ │                                 │ │
│ │   No cache (Redis)              │ │
│ └─────────────────────────────────┘ │
└─────────────────────────────────────┘
```

### AFTER (PHASE 3) - Professional Integrated System:
```
┌────────────────────────────────────────────────────────┐
│       Docker-Compose Network (Automatic Network)       │
│                                                        │
│  ┌────────────┐   ┌─────────────┐   ┌──────────┐       │
│  │  Django    │◄─►│ PostgreSQL  │   │  Redis   │       │
│  │    App     │   │   Database  │   │  Cache   │       │
│  │ :3000      │   │   :5432     │   │  :6379   │       │
│  └────────────┘   └─────────────┘   └──────────┘       │
│        ▲                  ▲                ▲           │
│        └──────────────────┼────────────────┘           │
│                 Automatic DNS Network                  │
│                                                        │
│                                                        │
│  Each service can scale, restart, update itself       │
│  without affecting others. Everything synchronized.    │
└────────────────────────────────────────────────────────┘
```

---

**Everything works integrated automatically.**

### Smart Networks Between Containers
Containers communicate with each other automatically:
- Django accesses PostgreSQL: `postgresql://db:5432/...`
- Django accesses Redis: `redis://cache:6379/...`
- Nginx talks with Django: `http://web:3000`

**No IP configuration, no complications. Pure Docker magic.**

### Development = Production
What you see on your PC is exactly what runs on the server:
```
Local (docker-compose up) 
    ↓
Testing  
    ↓
Production (docker-compose.prod up)

Same config = Same results = No surprises
```

### Enormously Facilitates Production
- ✅ Works the same on AWS, DigitalOcean, dedicated server
- ✅ Databases, cache, queues, everything integrated
- ✅ Centralized and monitored logs
- ✅ Automatic backups
- ✅ Easy SSL/HTTPS



---

## STEP 1: Create the `docker-compose.yml` file

In your `project/` folder, create a new file called `docker-compose.yml` (at the same level as the Dockerfile).

### Option A: Create file via Terminal (recommended)

**Windows (PowerShell):**
```powershell
@'
version: '3.8'

services:
  web:
    build: .
    image: image_project:v1.0
    container_name: container_project
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
    image: image_project:v1.0
    container_name: container_project
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

### Option B: Create manually

1. Open VS Code in your `project/` folder
2. Right-click in explorer → **"New File"**
3. Name it: `docker-compose.yml`
4. Copy the content from the next block into the file

### ▶️ File Content

If you used **Option A (Terminal)**, you're done! ✅  
If you used **Option B (VS Code)**, copy this exact content:

```yaml
version: '3.8'

services:
  web:
    build: .
    image: image_project:v1.0
    container_name: container_project
    command: python manage.py runserver 0.0.0.0:3000
    volumes:
      - .:/usr/src/app
    ports:
      - "3000:3000"
    environment:
      - PYTHONUNBUFFERED=1
      - PYTHONDONTWRITEBYTECODE=1
```

### Line by Line - YAML Explained:

| Line | What it means | Why it matters | Scalability |
|------|--------------|-----------------|-------------|
| `version: '3.8'` | Docker-compose version | Compatible with modern Docker | Supports all features you'll need |
| `services:` | DEFINE ALL YOUR CONTAINERS HERE | Growth point: today the web app, in future (another app, db, cache, nginx, backup) | You can have unlimited services running together |
| `web:` | Name of Django service | Unique identifier. Later: `db:`, `cache:`, etc. | Each service scales, restarts independently |
| `build: .` | Builds from Dockerfile in this folder | Uses existing Dockerfile you created | You can have multiple Dockerfiles for different services |
| `image: image_project:v1.0` | Image name with version | Identifies exact generated image | Facilitates versioning and reuse |
| `container_name: container_project` | Container name | Reusable, easy to identify with `docker ps` | Easy debugging and monitoring - same name in all commands |
| `command:` | Command to execute on startup | Starts Django automatically | Each service runs its own command |
| `volumes:` | Syncs folders PC ↔ container | Code changes visible instantly (hot-reload) | Data persists when container restarts |
| `- .:/usr/src/app` | Your PC ↔ /usr/src/app in container | Files synchronized in real time | Same pattern for DB: PostgreSQL saves data in volume |
| `ports:` | Port mapping | App access from browser | Django:3000, Nginx:80, PostgreSQL:5432, Redis:6379 |
| `- "3000:3000"` | Port 3000 local ↔ Port 3000 container | `localhost:3000` will open the app | Each service has its own ports |
| `environment:` | Environment variables | Configurations, credentials, connections | DATABASE_URL, REDIS_URL, secret keys (next) |
| `PYTHONUNBUFFERED=1` | Logs in real time without buffer | See errors immediately in terminal | Critical for debugging in production |
| `PYTHONDONTWRITEBYTECODE=1` | Doesn't create `.pyc` files | Less clutter + smaller volume | Improves sync performance |

✅ **Result:** Every time you run `docker-compose up`, it uses the SAME image and SAME container (reusability, fewer resources)

---

## STEP 2: Start Your Application with Docker-Compose

### First time: Run `docker-compose up`

Open Terminal in your `project/` folder (where the `docker-compose.yml` is) and run:

**Windows (PowerShell):**
```powershell
docker-compose up
```

**macOS / Linux (Bash):**
```bash
docker-compose up
```

### What Happens Automatically?

```
1️⃣ Docker checks if image exists: image_project:v1.0
                    ↓
2️⃣ If NOT → Automatically runs: docker build
                    ↓
3️⃣ Creates container: container_project
                    ↓
4️⃣ Starts Django at http://localhost:3000
                    ↓
5️⃣ See logs live in your terminal
```

### ✅ Expected Result:

In your terminal you'll see something like:
```
[+] Running 1/1
 ✔ Container container_project  Created
Attaching to container_project
container_project  | Watching for file changes with StatReloader
container_project  | Starting development server at http://0.0.0.0:3000/
container_project  | Quit the server with CONTROL-C.
```

### 🌐 Open Your Browser:

Go to: **http://localhost:3000/**

You should see your website working! 

### ⏹️ To Stop:

Press in terminal: **`Ctrl + C`**

---

## Useful `docker-compose up` Commands

After the first time, each time you want to start your app:

**Option A: In foreground (see logs in terminal)**
```bash
docker-compose up
```

**Option B: In background (free up terminal)**
```bash
docker-compose up -d
```

Then, to see logs anytime:
```bash
docker-compose logs -f web
```

### When Do You Need to Rebuild?

Use `docker-compose build` ONLY if:
- ✅ You change `requirements.txt` (new Python packages)
- ✅ You change `Dockerfile` (new configuration)
- ✅ You want to force rebuild (clear cache)

### You DON'T Need to Rebuild if:
- ❌ You change Python files (views.py, models.py, etc.)
- ❌ You change HTML templates
- ❌ You change CSS or JavaScript
- ❌ You change static files

### Command to Rebuild:

```bash
docker-compose build
```

Then start again:
```bash
docker-compose up
```

Or in one command:
```bash
docker-compose up --build
```

---

### Most Common Commands:

| Command | What it does | Example |
|---------|-------------|---------|
| `docker-compose up` | Start all services (view logs) | `docker-compose up` |
| `docker-compose up -d` | Start in background (no logs) | `docker-compose up -d` |
| `docker-compose down` | Stop and remove containers | `docker-compose down` |
| `docker-compose logs -f web` | View logs in real time | `docker-compose logs -f web` |
| `docker-compose build` | Rebuild image | `docker-compose build` |
| `docker-compose exec web bash` | Access container terminal | `docker-compose exec web bash` |
| `docker-compose ps` | View service status | `docker-compose ps` |
| `docker-compose restart` | Restart all services | `docker-compose restart` |

---

## ✨ What You Learned in PHASE 3

### Key Concepts:
✅ Docker-Compose is the professional standard for Django  
✅ ONE YAML file defines EVERYTHING in your system  
✅ Multiple services communicate automatically  
✅ Volumes enable fast development (hot-reload)  
✅ Same file for development, testing, and production  
✅ Scalable from simple to complex  

### Skills Acquired:
✅ Create and understand `docker-compose.yml`  
✅ Run multiple coordinated containers  
✅ Use Docker automatic networks  
✅ Data persistence with volumes  
✅ Environment variables for configuration  
✅ Preparation for production  

---

## 🚀 Next Steps:

### Intermediate Level (With Docker-Compose):
- ✅ Add PostgreSQL as database 
- ✅ Add Redis for cache and sessions
- ✅ Configure Nginx as reverse proxy
- ✅ Add automatic SSL/HTTPS
- ✅ Automatic backup system

### Advanced Level (Complete Application):
- ✅ Add contact forms
- ✅ User system and authentication
- ✅ Professional admin dashboard
- ✅ REST API with Django REST Framework
- ✅ Email notification system

### Production (Professional Scale):
- ✅ Switch to gunicorn (professional server, not dev)
- ✅ `.env` file for secret credentials
- ✅ CI/CD with GitHub Actions
- ✅ Automatic error monitoring
- ✅ Daily automatic backups
- ✅ Deploy to AWS, DigitalOcean, Heroku, Azure
- ✅ Automatic SSL certificates with Let's Encrypt

---

## Complete Glossary - Key Terms

## 📚 Complete Glossary - Key Terms 

| Term | Meaning | In Your Project |
|------|---------|-----------------|
| **HTML** | Language to create web page structures | templates/base.html |
| **CSS** | Language to make pages look beautiful | static/css/style.css |
| **JavaScript** | Language to make pages interactive | static/js/menu.js |
| **Django** | Python framework (tool) for creating professional websites | djangoProject/ |
| **Docker** | Container - packages your application to run on any PC | Dockerfile |
| **Image** | Docker template/recipe (like an .ISO) | `image_project:v1.0` |
| **Container** | Instance running the image (like an active virtual machine) | `container_project` |
| **Tag/Label** | Version or variant of an image | `v1.0` in `image_project:v1.0` |
| **Dockerfile** | File that defines how to build the image | PHASE 1, STEP 3 |
| **Docker-Compose** | Tool for defining and running multiple containers with YAML file | docker-compose.yml |
| **YAML** | Human-readable file format (uses spaces and colons, not brackets) | docker-compose.yml |
| **Build** | Compile Dockerfile to create an image | `docker build` / `docker-compose build` |
| **Service** | Individual service in docker-compose (in your case: "web") | services: web: |
| **Template** | HTML file that Django fills with data (dynamic) | templates/home.html |
| **View** | Python function that processes data and returns a template | web/views.py |
| **URL** | Web address (http://localhost:3000/) | web/urls.py |
| **Navbar** | Navigation bar (menu) | templates/header.html |
| **Responsive** | Adapts to mobile, tablets, desktops | CSS with media queries |
| **Hot-Reload** | Code changes visible automatically without restart | Volume + PYTHONUNBUFFERED=1 |
| **Volume** | Folder sync between PC and Docker container | `.:/usr/src/app` in docker-compose.yml |
| **Port Mapping** | Connection PC port ↔ container port | `-p 3000:3000` |
| **Environment Variables** | Configurations passed to container | `PYTHONUNBUFFERED=1` |
| **Versioning** | Version control of the image | `v1.0`, `v2.0`, etc. |

---

## 🎓 Want to Learn More?

- [Django Official](https://www.djangoproject.com/)
- [MDN Web Docs (HTML/CSS/JS)](https://developer.mozilla.org/)
- [Docker Official](https://www.docker.com/)

---

## 🎉 Congratulations! Your Complete Guide is Ready

You now have a complete Django + Docker professional website. From basic setup to production-ready architecture with Docker-Compose. Keep learning and building!

