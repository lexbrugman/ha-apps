ARG BUILD_FROM=ghcr.io/home-assistant/base-python:3.14-alpine3.23@sha256:22a20043ded03472ec1fcac3137e97aa209f24621257531dcac45a0ac4b57c1d
FROM ${BUILD_FROM}

WORKDIR /opt/evohome-helper

COPY ./rootfs/. ./

RUN chmod +x ./run.sh ./src/main.py
RUN pip3 install --no-cache-dir poetry \
    && poetry config virtualenvs.create false \
    && poetry install --only main --no-root --no-interaction --no-ansi

CMD [ "./run.sh" ]
