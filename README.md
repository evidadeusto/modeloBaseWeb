# 🌐 modeloBaseWeb

### Professional Website Template with Django + Docker

> **A solid starting point for building modern, scalable, and professional web applications.**

[![Django](https://img.shields.io/badge/Django-4.2+-092E20?style=for-the-badge&logo=django&logoColor=white)](https://www.djangoproject.com/)
[![Docker](https://img.shields.io/badge/Docker-Latest-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

## What is modeloBaseWeb?

`modeloBaseWeb` is a **professional and scalable template** for creating functional websites using **Django** (Python framework) and **Docker** (containers). It includes a complete base structure, development best practices, and step-by-step documentation to take you from zero to a production web project.

**Perfect for:**
- ✅ Developers who want a professional starting point
- ✅ Teams that need to standardize their Django projects
- ✅ Web applications that require Docker from the start
- ✅ Rapid prototyping with scalable architecture

---

## Visual Support

### 🏠 Home Page
![Homepage](/assets/imagesReadme/homepage.png)

### 📊 Administration Panel
![Admin Panel](/assets/imagesReadme/admin-panel.png)

### 📱 Responsive Design
![Mobile View](/assets/imagesReadme/mobile-view.png)

---

## 🚀 Quick Start (5 Steps)

### Prerequisites
- **Docker Desktop** — [Download](https://www.docker.com/products/docker-desktop)
- **Visual Studio Code** — [Download](https://code.visualstudio.com/download)
- **Git** — [Download](https://git-scm.com/)

### Step 1: Clone the Repository

```bash
git clone https://github.com/JULIAMGUERRERO/modeloBaseWeb.git
cd modeloBaseWeb
```

### Step A: Build the Docker Image (First time only)

```bash
docker-compose build --no-cache
```

This creates the image with the tag `project_image:v1.0` automatically based on the `docker-compose.yml` configuration.

**Verify it was created correctly:**
```bash
docker images
```

You should see `project_image` with tag `v1.0` in the list.

### Step B: Synchronize the Database (Migrations)

```bash
docker-compose run web python manage.py migrate
```

This command:
- 🔄 Synchronizes the database schema
- 📝 Applies all pending migrations
- ✅ Prepares the DB to use the project

### Step C: Create Superuser (Administrator)

```bash
docker-compose run web python manage.py createsuperuser
```

It will ask for:
- **Username:** Your admin username
- **Email:** Your email
- **Password:** Your password (hidden when typing)
- **Password (again):** Confirm password

### Step 2: Start the Server

```bash
docker-compose up
```

**You will see something like:**
```
Starting modelobaseweb_web_1 ... done
Starting modelobaseweb_db_1 ... done
Starting modelobaseweb on port 3000...
```

**Access your site:** http://localhost:3000

**Administration panel:** http://localhost:3000/admin (use your superuser credentials)

---

## Project Structure

```
modeloBaseWeb/
├──project
|    ├──djangoProject
|    │   ├── settings.py         # Project configuration
|    │   ├── urls.py             # Main routes
|    │   ├── wsgi.py             # WSGI interface
|    │   └── asgi.py             # ASGI interface
|    |
|    ├── web/                    # Your first Django application
|    |   ├── migrations/         # Database migration history
|    |   |   └──_init_.py        #
|    |   ├── static/             # Static files (CSS, JS, images)
|    |   |   └── ...             # folders: css, files, fonts, icons, img, js, media
|    |   ├── templates/          # HTML templates
|    |   |   └── includes        # template inheritance
|    |   ├── admin.py            # Administration panel
|    |   ├── apps.py             # 
|    │   ├── models.py           # DB models
|    |   ├── tests.py            # 
|    │   ├── urls.py             # App routes
|    │   └── views.py            # Business logic
|    |
|    ├── docker-compose.yml      # Service orchestration
|    ├── Dockerfile              # Container configuration
|    ├── manage.py               # Django main file
|    ├── requirements.txt        # Dependencies to install
|    ├── .gitignore              # Files to ignore in git
|    ├── README.md               # This file

```

---

## 📖 Complete Documentation

For a detailed **step-by-step** guide, check:
→ [**GUIDE.MD**](./GUIDE.MD)

In this guide you will find:
- **PHASE 1** → Basic structure (Django + Docker)
- **PHASE 2** → Create your first functional web page
- **PHASE 3** → Docker-Compose for professional projects

---

## 🛠️ Included Technologies

| Technology | Description |
|-----------|-----------|
| **Django 4.2+** | High-level web framework in Python |
| **Docker** | Containerization for consistent development |
| **Python 3.10+** | Programming language |

---

## 🔧 Advanced Configuration

### Using Docker Compose (Recommended)

```bash
docker-compose up --build
```

**This automatically starts:**
- ✅ Django server (port 3000)
- ✅ PostgreSQL database
- ✅ Nginx as reverse proxy (port 80)
- ✅ Persistent volumes for data

### Alternate Flow (If you need to make code changes)

**Terminal 1 - Start the server:**
```bash
docker-compose up
```

**Terminal 2 - Run commands in parallel:**
```bash
# Make migrations while server is running
docker-compose exec web python manage.py makemigrations

# Apply migrations
docker-compose exec web python manage.py migrate

# View logs
docker-compose logs -f web
```

### Environment Variables

Create a `.env` file in the project root:

```env
DEBUG=False
SECRET_KEY=your-secret-key-here
DATABASE_URL=postgres://user:password@db:5432/modelobaseweb
ALLOWED_HOSTS=localhost,127.0.0.1,yourdomain.com
```

---

## 📋 Daily Useful Commands

### Start/Stop the Server

```bash
# Start in foreground (see logs in real time)
docker-compose up

# Start in background (daemon mode)
docker-compose up -d

# Stop the server
docker-compose down

# View logs in real time
docker-compose logs -f web
```

### Working with the Database

```bash
# Create migrations (after changes in models.py)
docker-compose exec web python manage.py makemigrations

# Apply pending migrations
docker-compose exec web python manage.py migrate

# View migration status
docker-compose exec web python manage.py showmigrations
```

### Project Administration

```bash
# Create new superuser
docker-compose exec web python manage.py createsuperuser

# Access Django interactive shell
docker-compose exec web python manage.py shell

# Run tests
docker-compose exec web python manage.py test

# Collect static files
docker-compose exec web python manage.py collectstatic --noinput
```

### Container Maintenance

```bash
# Rebuild the image (without cache)
docker-compose build --no-cache

# Remove containers and volumes (⚠️ Deletes data)
docker-compose down -v

# View services status
docker-compose ps

# Enter container bash
docker-compose exec web bash
```

---

## 🌱 Next Steps

Once you have the project running:

1. **Customize the views** — Edit `myapp/views.py`
2. **Design your templates** — Create HTML in `myapp/templates/`
3. **Define your models** — Structure your database in `myapp/models.py`
5. **Deploy to production** — Use Docker Compose on your server

---

## 🤝 Contributions

Do you have improvements or suggestions for the template?

**I invite you to collaborate!**

- 🐛 **Report bugs** — [Issues](https://github.com/evidadeusto/modeloBaseWeb/issues)
- 🔀 **Make pull requests** — Your contributions are welcome

---

## 📄 License

This project is distributed under the **MIT** license. You are free to use, modify, and distribute the code, as long as you maintain the mention of the original license.

---


⭐ **If this project is useful to you, help others by leaving a star on GitHub** ⭐

## 💬 Connect With Me

Questions, suggestions, or simply want to share how you use this template?

💼 **LinkedIn:** [Juliam Guerrero Diaz](https://www.linkedin.com/in/juliamguerrero/)

📧 **Email:** [juliamdario.g@deusto.es](mailto:juliamdario.g@deusto.es)

🐙 **GitHub:** [@JULIAMGUERRERO](https://github.com/JULIAMGUERRERO)