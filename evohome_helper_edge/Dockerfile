ARG BUILD_FROM=ghcr.io/home-assistant/base-python:3.14-alpine3.23@sha256:7af3473d769217d2ea7f8a3b185757b2bae769abf274668f9c4fd9ad4ae77994
FROM ${BUILD_FROM}

WORKDIR /opt/evohome-helper

COPY ./rootfs/. ./

RUN chmod +x ./run.sh ./src/main.py
RUN pip3 install --no-cache-dir poetry \
    && poetry config virtualenvs.create false \
    && poetry install --only main --no-root --no-interaction --no-ansi

CMD [ "./run.sh" ]
