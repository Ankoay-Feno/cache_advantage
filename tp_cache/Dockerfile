# Stage 1: Builder for dependencies installation
FROM python:3.9-alpine AS builder

WORKDIR /app

RUN apk add --no-cache gcc g++ musl-dev libffi-dev openblas lapack-dev

ARG PIP_CACHE_DIR=~/.cache/pip
RUN mkdir -p ${PIP_CACHE_DIR}

# Use mount to persist pip cache across builds
RUN --mount=type=cache,target=${PIP_CACHE_DIR} \
    pip install --cache-dir=${PIP_CACHE_DIR} -r requirements.txt

# Stage 2: Image with cached dependencies
FROM python:3.9-alpine AS with_cache

WORKDIR /app

COPY . .

# Copy pip cache from the builder stage
COPY --from=builder /root/.cache/pip /root/.cache/pip

RUN pip install --no-index --find-links=/root/.cache/pip -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

# Stage 3: Image without caching
FROM python:3.9-alpine AS without_cache

WORKDIR /app

COPY . .

RUN apk add --no-cache gcc g++ musl-dev libffi-dev openblas lapack-dev

RUN pip install -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
