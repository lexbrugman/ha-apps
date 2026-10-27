ARG BUILD_FROM=ghcr.io/home-assistant/base-python:3.14-alpine3.23@sha256:abf518d8aaaf325297d97d29404927b2ec1e0bd95eb568edb8f0c9f9bdb5eb4d
FROM ${BUILD_FROM}

WORKDIR /opt/evohome-helper

COPY ./rootfs/. ./

RUN chmod +x ./run.sh ./src/main.py
RUN pip3 install --no-cache-dir poetry \
    && poetry config virtualenvs.create false \
    && poetry install --only main --no-root --no-interaction --no-ansi

CMD [ "./run.sh" ]
