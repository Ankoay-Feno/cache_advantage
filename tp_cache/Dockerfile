FROM python:3.9-alpine AS with_cache

WORKDIR /app

COPY . .

RUN apk add --no-cache gcc g++ musl-dev libffi-dev openblas lapack-dev

ARG PIP_CACHE_DIR=/root/.cache/pip
COPY --from=builder ${PIP_CACHE_DIR} ${PIP_CACHE_DIR}

RUN pip install --no-index --find-links=${PIP_CACHE_DIR} -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]



FROM python:3.9-alpine AS without_cache

WORKDIR /app

COPY . .

RUN apk add --no-cache gcc g++ musl-dev libffi-dev openblas lapack-dev

RUN  pip install -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]