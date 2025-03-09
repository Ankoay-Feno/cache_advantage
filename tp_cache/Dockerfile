FROM python:3.9-alpine AS with_cache

WORKDIR /app

COPY . .

ARG PIP_CACHE_DIR=/root/.cache/pip
RUN --mount=type=cache,target=${PIP_CACHE_DIR} pip install -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

FROM python:3.9-alpine AS without_cache

WORKDIR /app

COPY . .

ARG PIP_CACHE_DIR=/root/.cache/pip
RUN --mount=type=cache,target=${PIP_CACHE_DIR} pip install -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]