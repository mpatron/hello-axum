# Rust - Tokio/Axum

~~~bash
cargo add axum tower-http tracing tracing-subscriber tokio serde serde_json hyper-util http_body_util mime@0.3 \
--features tokio/full \
--features hyper-util/client \
--features hyper-util/http1 \
--features hyper-util/client-legacy \
--features tower-http/trace \
--features tracing-subscriber/env-filter \
&& cargo update --verbose
cargo add --dev tower --features tower/util && cargo update --verbose
cargo clean && cargo build && cargo test
~~~

~~~bash
cargo make
podman image ls --all
podman run --detach --rm --publish 3000:3000 --name server --network=podman mpatron/server:latest
~~~

Dans un terminal

~~~bash
podman logs --follow server
~~~

Dans un autre

~~~bash
podman exec -it server curl localhost:3000
podman exec -it server curl localhost:3000/requires-connect-info
~~~

https://www.julienrollin.com/posts/rust-axum-part-1
