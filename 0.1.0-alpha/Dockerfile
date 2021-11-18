FROM rust:1.54 AS builder

ENV KAIROI_DOWNLOAD_URL https://github.com/emerick42/kairoi/archive/refs/tags/v0.1.0-alpha.tar.gz

RUN set -eux; \
    wget -O kairoi.tar.gz "$KAIROI_DOWNLOAD_URL"; \
    mkdir -p /usr/src/kairoi; \
    tar -xzf kairoi.tar.gz -C /usr/src/kairoi --strip-components=1; \
	cargo build --release --manifest-path /usr/src/kairoi/Cargo.toml

FROM debian:bullseye-slim

COPY --from=builder /usr/src/kairoi/target/release/kairoi /usr/local/bin/kairoi

RUN mkdir -p /var/lib/kairoi
WORKDIR /var/lib/kairoi

VOLUME /var/lib/kairoi

EXPOSE 5678
ENTRYPOINT ["kairoi"]
