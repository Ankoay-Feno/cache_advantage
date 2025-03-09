# Stage: Builder
FROM python:3.9-alpine AS builder

WORKDIR /app

# Installe les outils nécessaires pour compiler les paquets Python
RUN apk add --no-cache gcc g++ musl-dev libffi-dev openblas lapack-dev make clang

# Copie le fichier requirements.txt
COPY requirements.txt .

# Installe les dépendances avec pip
RUN pip install --no-cache-dir -r requirements.txt

# Stage with_cache: Utilise les dépendances installées et copie le reste du projet
FROM python:3.9-alpine AS with_cache

WORKDIR /app

# Copie l'ensemble de l'application
COPY . .

# Installe les dépendances si le cache n'est pas déjà présent
RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 8000

# Démarre l'application Django
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

# Stage without_cache: Installation sans cache
FROM python:3.9-alpine AS without_cache

WORKDIR /app

# Installe les outils nécessaires pour compiler les paquets Python
RUN apk add --no-cache gcc g++ musl-dev libffi-dev openblas lapack-dev make clang

# Copie l'ensemble de l'application
COPY . .

# Installe les dépendances sans utiliser le cache pip
RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 8000

# Démarre l'application Django
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
