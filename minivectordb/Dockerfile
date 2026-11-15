# ---- build stage ----
FROM rust:1.83-slim-bookworm AS build
WORKDIR /src
COPY Cargo.toml ./
COPY src ./src
RUN cargo build --release

# ---- runtime stage ----
FROM debian:bookworm-slim
RUN apt-get update \
 && apt-get install -y --no-install-recommends ca-certificates \
 && rm -rf /var/lib/apt/lists/*
WORKDIR /app
COPY --from=build /src/target/release/mvdb /app/mvdb
ENV MVDB_DATA=/data
VOLUME ["/data"]
ENTRYPOINT ["/app/mvdb"]
