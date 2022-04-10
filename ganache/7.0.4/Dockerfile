FROM node:14-slim AS builder

RUN apt-get update && apt-get install -y build-essential python && rm -rf /var/lib/apt/lists/*

RUN groupadd -r ganache && useradd -r -g ganache ganache
RUN mkdir -p /home/ganache && chown -R ganache:ganache /home/ganache
USER ganache
WORKDIR /home/ganache

RUN npm install ganache@7.0.4

FROM node:14-slim

RUN groupadd -r ganache && useradd -r -g ganache ganache
RUN mkdir -p /home/ganache && chown -R ganache:ganache /home/ganache
USER ganache
WORKDIR /home/ganache

COPY --from=builder /home/ganache/node_modules node_modules

ENTRYPOINT ["/home/ganache/node_modules/.bin/ganache"]