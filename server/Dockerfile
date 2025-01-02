FROM docker.io/rust:1.83-slim as builder
WORKDIR /usr/src/myapp
COPY . .
RUN cargo build --release
RUN cargo install --verbose --path .

FROM docker.io/ubuntu:24.04
RUN apt-get update -y \
    && apt-get install -y --no-install-recommends openssl ca-certificates ncat curl \
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* 
# Ne fonctionne pas encore avec alpine. L'image passerait de 86Mo à 11Mo...
# FROM alpine:3.19.1
# RUN apk add --no-cache ca-certificates netcat-openbsd libgcc libstdc++ libc6-compat

COPY --from=builder /usr/src/myapp/target/release/server /usr/local/bin/server

RUN adduser \
  --disabled-password \
  --gecos "" \
  --home "/nonexistent" \
  --shell "/sbin/nologin" \
  --no-create-home \
  --uid "10001" \
  appuser
RUN chown -R appuser /usr/local/bin/server
USER appuser
# ENV RUST_LOG="server=debug,info"
WORKDIR /usr/local/bin/

EXPOSE 3000
CMD [ "/usr/local/bin/server" ]
# CMD ["/bin/sleep 3650d"]
