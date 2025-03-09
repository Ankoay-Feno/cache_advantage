FROM python:3.9-alpine AS with_cache

WORKDIR /app

COPY . .

RUN apk add --no-cache gcc g++ musl-dev libffi-dev openblas lapack-dev

ENV PATH=".env/bin:$PATH"

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

FROM python:3.9-alpine AS without_cache

WORKDIR /app

COPY . .

RUN apk add --no-cache gcc g++ musl-dev libffi-dev openblas lapack-dev

RUN  pip install -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]