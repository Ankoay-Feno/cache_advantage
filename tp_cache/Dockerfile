(.env) ankoayfeno@cloudshell:~/cache_advantage/tp_cache$ cat Dockerfile 
FROM python:3.12-slim AS compile-image
RUN apt-get update
RUN apt-get install -y --no-install-recommends build-essential gcc

RUN python -m venv /opt/venv

ENV PATH="/opt/venv/bin:$PATH"

COPY requirements.txt .
RUN pip install -r requirements.txt


FROM python:3.12-slim AS with_cache
COPY --from=compile-image /opt/venv /opt/venv

ENV PATH="/opt/venv/bin:$PATH"

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

FROM python:3.9-alpine AS without_cache

WORKDIR /app

COPY . .

RUN apk add --no-cache gcc g++ musl-dev libffi-dev openblas lapack-dev

RUN  pip install -r requirements.txt

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

(.env) ankoayfeno@cloudshell:~/cache_advantage/tp_cache$ docker run --rm -it -p 8000:8000 --name my_container image-with-cache 
python: can't open file '//manage.py': [Errno 2] No such file or directory
exit status 2