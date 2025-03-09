FROM python:3.11.10-slim-bullseye AS with_cache

WORKDIR /app


COPY tp_cache .

COPY /usr/local/lib/python3.11/site-packages/ /usr/local/lib/python3.11/site-packages/

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

FROM python:3.9-alpine AS without_cache

WORKDIR /app

RUN apk add --no-cache gcc g++ musl-dev libffi-dev openblas lapack-dev make clang

COPY . .

RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
