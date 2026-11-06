ARG BUILD_FROM=ghcr.io/home-assistant/base-python:3.15-alpine3.23@sha256:a65aa92b295f04d497886db634345291580254befbc05a7b3873986e3c916a48
FROM ${BUILD_FROM}

WORKDIR /opt/evohome-helper

COPY ./rootfs/. ./

RUN chmod +x ./run.sh ./src/main.py
RUN pip3 install --no-cache-dir poetry \
    && poetry config virtualenvs.create false \
    && poetry install --only main --no-root --no-interaction --no-ansi

CMD [ "./run.sh" ]
