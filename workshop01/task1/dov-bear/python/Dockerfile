# node 21
FROM python:3.9-slim-buster AS Builder

#create /app and cd into /app
RUN mkdir /app
WORKDIR /app

# inside /app

COPY main.py .
COPY util.py .
COPY run.sh .
COPY requirements.txt .
COPY public public
COPY templates templates

# install dependancies, && to run another command after first command
RUN apt-get update && apt-get install -y \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

RUN apt install -curl

RUN python3.9 -m pip install --no-cache-dir --upgrade \
    pip \
    setuptools \
    wheel
RUN python3.9 -m pip install --no-cache-dir \
    -r requirements.txt

## RUN

HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
    CMD curl -s http://localhost:${APP_PORT}/healthz || exit 1

ENV PORT=5000 INSTANCE_NAME="PYTHON Dov Bear" INSTANCE_HASH=abc123

EXPOSE ${APP_PORT}

ENTRYPOINT python main.py