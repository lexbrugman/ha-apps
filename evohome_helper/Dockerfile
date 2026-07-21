ARG BUILD_FROM=ghcr.io/home-assistant/base-python:3.14-alpine3.23@sha256:66f223ca04b4053a59d24ff210518112465c3c3166b1967473cb2642a4462cab
FROM ${BUILD_FROM}

WORKDIR /opt/evohome-helper

COPY ./rootfs/. ./

RUN chmod +x ./run.sh ./src/main.py
RUN pip3 install --no-cache-dir poetry \
    && poetry config virtualenvs.create false \
    && poetry install --only main --no-root --no-interaction --no-ansi

CMD [ "./run.sh" ]
