# Builder stage: Utilise un environnement pour installer les dépendances avec cache
FROM python:3.9-alpine AS builder

WORKDIR /app

# Installe les outils nécessaires pour compiler les paquets Python qui en ont besoin
RUN apk add --no-cache gcc g++ musl-dev libffi-dev openblas lapack-dev

# Copie uniquement le fichier requirements.txt pour optimiser le cache Docker
COPY requirements.txt .

# Vérifie si requirements.txt est bien copié dans l'image Docker
RUN ls -l /app

# Installe les dépendances Python avec pip et le cache
RUN pip install --no-cache-dir -r requirements.txt

# Stage with_cache: Utilise les dépendances installées et copie le reste du projet
FROM python:3.9-alpine AS with_cache

WORKDIR /app

# Copie le reste de l'application
COPY . .

# Vérifie à nouveau si requirements.txt est présent dans l'image
RUN ls -l /app

# Installe les dépendances si le cache n'est pas déjà présent
RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 8000

# Démarre le serveur Django
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

# Stage without_cache: Si vous voulez forcer l'installation sans cache
FROM python:3.9-alpine AS without_cache

WORKDIR /app

# Installe les outils nécessaires pour compiler les paquets Python qui en ont besoin
RUN apk add --no-cache gcc g++ musl-dev libffi-dev openblas lapack-dev

# Copie le reste de l'application
COPY . .

# Vérifie à nouveau si requirements.txt est présent dans l'image
RUN ls -l /app

# Installe les dépendances sans utiliser le cache pip
RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 8000

# Démarre le serveur Django
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
