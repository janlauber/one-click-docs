# Builds

## CI

Each CI/CD pipeline has its own syntax and configuration. Below are examples for GitHub Actions and Gitlab Pipelines.

### Github Actions

```yaml
name: Docker Image Build & Push

on:
  release:
    types: [created]

env:
  REGISTRY: ghcr.io
  IMAGE_NAME: ${{ github.repository }}

jobs:
  build-and-push-image:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Log in to the Container registry
        uses: docker/login-action@65b78e6e13532edd9afa3aa52ac7964289d1a9c1
        with:
          registry: ${{ env.REGISTRY }}
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Extract metadata (tags, labels) for Docker
        id: meta
        uses: docker/metadata-action@9ec57ed1fcdbf14dcef7dfbe97b2010124a938b7
        with:
          images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}

      - name: Build and push Docker image
        uses: docker/build-push-action@f2a1d5e99d037542a71f64918e516c093c6f3fc4
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
```

### Gitlab Pipelines

```yaml
stages:
  - build
  - push

variables:
  DOCKER_VERSION: 25.0.2

before_script:
  - export IMAGE_TAG="$CI_REGISTRY_IMAGE:$CI_COMMIT_TAG"
  - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY

services:
  - docker:$DOCKER_VERSION-dind

build_push:
  stage: build
  image: docker:$DOCKER_VERSION
  tags:
    - ti
  script:
    - docker build -t $IMAGE_TAG .
    - docker push $IMAGE_TAG
  only:
    - tags
```

## Dockerfiles

There are many ways to write a Dockerfile. Below are examples for Streamlit, Golang and Remix.js

### Streamlit

{% embed url="https://github.com/janlauber/one-click-demo" %}

```Dockerfile
ARG POETRY_VERSION=1.4

FROM python:3.12-slim as base
WORKDIR /streamlit
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONFAULTHANDLER=1 \
    PYTHONUNBUFFERED=1
EXPOSE 8501

FROM base as poetry
ARG POETRY_VERSION
ENV POETRY_CACHE_DIR=/opt/.poetry-cache \
    PIP_DEFAULT_TIMEOUT=100 \
    PIP_DISABLE_PIP_VERSION_CHECK=1 \
    PIP_IGNORE_INSTALLED=1 \
    PIP_NO_CACHE_DIR=1
# hadolint ignore=DL3013
RUN pip install --upgrade pip setuptools \
    && pip install poetry=="${POETRY_VERSION}"
COPY pyproject.toml poetry.lock* ./
# hadolint ignore=SC1091
RUN python -m venv /venv \
    && . /venv/bin/activate \
    && poetry install --only main \
    --no-root --no-interaction --no-ansi
COPY <<-EOT /entrypoint.sh
#!/usr/bin/env sh
set -e
. /venv/bin/activate
exec "\$@"
EOT

RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

FROM poetry as dev
# hadolint ignore=SC1091
RUN . /venv/bin/activate \
    && poetry install \
    --no-root --no-interaction --no-ansi
COPY . .
CMD ["streamlit", "run", "./app/🏠_Home.py"] # replace with your streamlit app

FROM base as prod
COPY --from=poetry /venv /venv
ENV PATH="/venv/bin:${PATH}"
COPY . .
CMD ["streamlit", "run", "./app/🏠_Home.py", "--server.port=8501", "--server.address=0.0.0.0"] # replace with your streamlit app
```

### Golang

```Dockerfile
FROM golang:1.22-alpine AS builder
WORKDIR /build
COPY go.mod go.sum main.go ./
RUN go mod tidy \
  && CGO_ENABLED=0 go build

FROM alpine:3.19 as runtime

RUN addgroup -S app \
    && adduser -S -G app app

WORKDIR /home/app
COPY --from=builder /build/app .
RUN chown -R app:app ./

USER app

CMD ["./app"]
```

### Remix.js

```Dockerfile
FROM node:20.2.0-alpine3.18 as base
FROM base as deps
WORKDIR /app
COPY package*.json ./
RUN npm install
FROM deps AS builder
WORKDIR /app
COPY . .
RUN npm run build
FROM deps AS prod-deps
WORKDIR /app
RUN npm install --production
FROM base as runner
WORKDIR /app
RUN addgroup --system --gid 1001 remix
RUN adduser --system --uid 1001 remix
USER remix
COPY --from=prod-deps --chown=remix:remix /app/package*.json ./
COPY --from=prod-deps --chown=remix:remix /app/node_modules ./node_modules
COPY --from=builder --chown=remix:remix /app/build ./build
COPY --from=builder --chown=remix:remix /app/public ./public
EXPOSE 3000
ENTRYPOINT [ "node", "node_modules/.bin/remix-serve", "build/index.js"]
```
