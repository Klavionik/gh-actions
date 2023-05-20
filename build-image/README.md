## Build Docker image

A GitHub composite action that builds a Docker image and pushes it to GitHub Container
Registry.

* Image template: `ghcr.io/<owner>/<repository>/<service>`.
* Caching: inline.

## Usage

```yaml
name: Build app images

on: [push]

jobs:
  build-app:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
    steps:
      - uses: Klavionik/gh-actions/build-image@main
        name: Build frontend service
        with:
          context: frontend
          service: frontend
          platform: linux/amd64
```

## Inputs

| Name        | Type   | Default                      | Description                     |
|-------------|--------|------------------------------|---------------------------------|
| `service`   | String | `app`                        | The last part of the image tag  |
| `context`   | String | `.` (root of the repository) | Docker build context            |
| `platforms` | String | `linux/arm64`                | Target platforms                |
