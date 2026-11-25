ARG BUILD_FROM=ghcr.io/home-assistant/base-python:3.15-alpine3.23@sha256:f7d375016c80da905fd4a9fa6cfa6ee4d58b5297518a9a63409776fab76541fd
FROM ${BUILD_FROM}

WORKDIR /opt/evohome-helper

COPY ./rootfs/. ./

RUN chmod +x ./run.sh ./src/main.py
RUN pip3 install --no-cache-dir poetry \
    && poetry config virtualenvs.create false \
    && poetry install --only main --no-root --no-interaction --no-ansi

CMD [ "./run.sh" ]
