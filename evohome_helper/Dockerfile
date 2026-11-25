ARG BUILD_FROM=ghcr.io/home-assistant/base-python:3.14-alpine3.23@sha256:599028fc12918d81efefb8685e5c41356b3651272ab18646236c134649b97231
FROM ${BUILD_FROM}

WORKDIR /opt/evohome-helper

COPY ./rootfs/. ./

RUN chmod +x ./run.sh ./src/main.py
RUN pip3 install --no-cache-dir poetry \
    && poetry config virtualenvs.create false \
    && poetry install --only main --no-root --no-interaction --no-ansi

CMD [ "./run.sh" ]
