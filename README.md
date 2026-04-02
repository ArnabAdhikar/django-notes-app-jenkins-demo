# Django Notes App with Jenkins CI/CD Demo

This project is a full-stack Notes application built with **Django** (Backend) and **React** (Frontend). It serves as a demonstration of a complete development workflow, including containerization with **Docker** and a CI/CD pipeline using **Jenkins**.

## 🚀 Project Overview

The application allows users to create, read, update, and delete (CRUD) notes. It features a modern React-based UI that communicates with a Django REST API. The entire stack is orchestrated using Docker and automated via Jenkins.

## 📂 Project Structure

```text
django-notes-app-jenkins-demo/
├── api/                # Django Application (REST API)
│   ├── migrations/     # Database migrations
│   ├── models.py       # Note model definition
│   ├── serializers.py  # DRF serializers
│   ├── urls.py         # API endpoint routing
│   └── views.py        # API view logic
├── mynotes/            # React Frontend Application
│   ├── public/         # Static assets
│   ├── src/            # React source code (components, pages, assets)
│   ├── Dockerfile      # Frontend containerization
│   └── package.json    # Node.js dependencies
├── notesapp/           # Main Django Project Configuration
│   ├── settings.py     # Global settings
│   ├── urls.py         # Main URL routing (serves React & API)
│   └── wsgi.py         # WSGI configuration
├── nginx/              # Nginx Configuration
│   ├── default.conf    # Reverse proxy settings
│   └── Dockerfile      # Nginx containerization
├── staticfiles/        # Collected static files (post-build)
├── docker-compose.yml  # Multi-container orchestration
├── Dockerfile          # Backend containerization
├── Jenkinsfile         # CI/CD Pipeline definition
├── manage.py           # Django management script
├── requirements.txt    # Python dependencies
└── .dockerignore       # Files to exclude from Docker build context
```

## 🛠️ Technologies Used

- **Backend**: Python, Django, Django REST Framework, Gunicorn, WhiteNoise.
- **Frontend**: JavaScript, React, React Router, CSS.
- **Database**: MySQL (Production/Docker), SQLite (Local/Development).
- **Web Server**: Nginx (Reverse Proxy).
- **DevOps**: Docker, Docker Compose, Jenkins.

## ⚙️ Getting Started

### Prerequisites

- Python 3.x
- Node.js & npm
- Docker & Docker Compose (optional, for containerized setup)

### Local Development (Manual Setup)

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/ArnabAdhikar/django-notes-app-jenkins-demo.git
    cd django-notes-app-jenkins-demo
    ```

2.  **Backend Setup:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    pip install -r requirements.txt
    python manage.py migrate
    python manage.py runserver
    ```

3.  **Frontend Setup:**
    ```bash
    cd mynotes
    npm install
    npm start
    ```
    The frontend will be available at `http://localhost:3000`.

### Dockerized Development

You can run the entire stack (Nginx, Django, MySQL) using Docker Compose:

```bash
docker-compose up --build
```

- **Frontend/Nginx**: `http://localhost`
- **Backend API**: `http://localhost:8000/api/`
- **Django Admin**: `http://localhost:8000/admin/`

### 🐋 Docker Optimization

The project includes a `.dockerignore` file to ensure that unnecessary files (like `__pycache__`, `node_modules`, and the database `data/` directory) are excluded from the Docker build context. This results in smaller image sizes, faster builds, and avoids permission errors when the database is running.

## 📡 API Endpoints

The backend provides the following REST API endpoints:

- `GET /api/` - List all available API routes.
- `GET /api/notes/` - Retrieve all notes.
- `POST /api/notes/create/` - Create a new note.
- `GET /api/notes/<id>/` - Retrieve a specific note.
- `PUT /api/notes/<id>/update/` - Update an existing note.
- `DELETE /api/notes/<id>/delete/` - Delete a note.

## 🏗️ CI/CD with Jenkins

The [Jenkinsfile](file:///home/arnab-adhikary/Downloads/django-notes-app-jenkins-demo/Jenkinsfile) defines a pipeline with the following stages:

1.  **Code Clone**: Pulls the latest code from GitHub.
2.  **Code Build**: Builds the Docker images for the application.
3.  **Push to DockerHub**: Pushes the built images to a Docker registry.
4.  **Deploy**: Deploys the application to the target environment.

## 📄 License

This project is open-source and available under the MIT License.
