# Home Assistant add-on build.
# BUILD_FROM is the HA arch-specific Alpine base (see build.json).
# The application code is pulled from the main repo at a pinned tag or branch,
# so this add-on repo stays thin and tracks MG4 Mate releases.
ARG BUILD_FROM
FROM ${BUILD_FROM}

# Version of Mate to install (git tag, branch or commit in the main repo/fork).
ARG MATE_REF=95f7e7c

ENV PYTHONUNBUFFERED=1 \
    DB_PATH=/data/mg4_mate.db

WORKDIR /app

# bash is needed by run.sh; build-deps are only needed to compile any wheel that
# lacks a musl build, and are removed in the same layer to keep the image small.
RUN apk add --no-cache bash \
    && apk add --no-cache --virtual .build-deps git build-base libffi-dev openssl-dev \
    && git clone https://github.com/ghianciulu/mg4-mate.git /src \
    && cd /src && git checkout "${MATE_REF}" \
    && pip install --no-cache-dir \
       -r /src/poller/requirements.txt \
       -r /src/web/requirements.txt \
    && cp -r /src/poller /src/web /app/ \
    && cp /src/run.sh /run.sh && chmod a+x /run.sh \
    && rm -rf /src \
    && apk del .build-deps

CMD ["/run.sh"]
