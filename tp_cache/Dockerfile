FROM python:3.13.2-alpine3.21 AS compile-image

RUN apk update && apk add --no-cache \
    build-base \
    gcc \
    g++ \
    python3-dev \
    py3-pip
WORKDIR /app
RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
COPY requirements.txt .
RUN pip install -r requirements.txt


# FROM python:3.12-slim AS compile-image
# RUN apt-get update
# RUN apt-get install -y --no-install-recommends build-essential gcc
# RUN python -m venv /opt/venv
# ENV PATH="/opt/venv/bin:$PATH"
# COPY requirements.txt .
# RUN pip install -r requirements.txt

FROM python:3.12-slim AS with_cache
COPY --from=compile-image /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
EXPOSE 8000
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]



FROM python:3.12-slim AS without_cache
COPY --from=compile-image /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
EXPOSE 8000
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
