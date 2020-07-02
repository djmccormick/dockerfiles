FROM postgres:12-alpine

ENV WAL2JSON_COMMIT_ID=92b33c7d7c2fccbeb9f79455dafbc92e87e00ddd

RUN apk update
RUN apk add --no-cache --virtual .build-deps clang clang-dev llvm gcc git make musl-dev pkgconf \
    && git clone https://github.com/eulerto/wal2json -b master --single-branch \
    && (cd /wal2json && git checkout $WAL2JSON_COMMIT_ID && USE_PGXS=1 make && USE_PGXS=1 make install) \
    && rm -rf wal2json \
    && apk del .build-deps

COPY /docker-entrypoint-initdb.d /docker-entrypoint-initdb.d
