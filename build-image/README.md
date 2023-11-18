## Build Docker image

A GitHub composite action that builds a Docker image and pushes it to GitHub Container
Registry.

* Image template: `ghcr.io/<owner>/<repository>/<service>`.
* Caching: S3 storage.

## Usage

```yaml
name: Build app images

on: [ push ]

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

| Name               | Type   | Default                       | Description                    |
|--------------------|--------|-------------------------------|--------------------------------|
| `service`          | String | `app`                         | The last part of the image tag |
| `context`          | String | `.` (root of the repository)  | Docker build context           |
| `platforms`        | String | `linux/arm64`                 | Target platforms               |
| `cache-endpoint`   | String | `s3.klavionik.dev`            | S3 endpoint URL                |
| `cache-region`     | String | `mos`                         | S3 region                      |
| `cache-bucket`     | String | -                             | S3 bucket to store build cache |
| `cache-access-key` | String | -                             | S3 access key                  |
| `cache-secret-key` | String | -                             | S3 secret key                  |
| `build-args`       | List   | -                             | Build-time arguments           |
| `tags`             | List   | -                             | Tags for the output image      |
