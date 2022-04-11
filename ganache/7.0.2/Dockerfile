FROM node:14-slim@sha256:f4e1b2eb7056213b394434a23d119523ed6171e54b1e7eff16fa0d86057395a9 AS builder

RUN apt-get update && apt-get install -y --no-install-recommends build-essential=12.3 python=2.7.13-2 && rm -rf /var/lib/apt/lists/*

WORKDIR /home/ganache
RUN groupadd -r ganache && useradd -r -g ganache ganache && chown -R ganache:ganache /home/ganache
USER ganache

RUN npm install ganache@7.0.2

FROM node:14-slim@sha256:f4e1b2eb7056213b394434a23d119523ed6171e54b1e7eff16fa0d86057395a9

WORKDIR /home/ganache
RUN groupadd -r ganache && useradd -r -g ganache ganache && chown -R ganache:ganache /home/ganache
USER ganache

COPY --from=builder /home/ganache/node_modules node_modules

ENTRYPOINT ["/home/ganache/node_modules/.bin/ganache"]