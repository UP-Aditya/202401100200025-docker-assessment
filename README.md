
## Stage 3 — Image Hardening and Vulnerability Scanning

### Security improvements
- Updated the base image to `python:3.13.18-slim-bookworm`.
- Upgraded Python dependencies to patched versions.
- Configured the application to run as a non-root user (UID 999).
- Upgraded pip, setuptools, and wheel during image construction.
- Built the hardened image as `fest-backend:0.2`.

### Trivy vulnerability scan results

| Image | Package type | Total findings | HIGH | CRITICAL |
|---|---|---:|---:|---:|
| fest-backend:0.1 | OS packages | 13,357 | 2,243 | 234 |
| fest-backend:0.1 | Python packages | 24 | 6 | 0 |
| fest-backend:0.2 | OS packages | 242 | 59 | 2 |
| fest-backend:0.2 | Python packages | 8 | 5 | 0 |

The OS and Python package findings are reported separately by Trivy.
The critical-vulnerability gate passed with exit code 0 using
`--severity CRITICAL --ignore-unfixed --exit-code 1`.

### Image size comparison

| Image | Size |
|---|---:|
| fest-backend:0.1 | 412 MB |
| fest-backend:0.2 | 53.3 MB |

The reported image size decreased by approximately 87%.

### Evidence
- `reports/trivy-before.txt`
- `reports/trivy-after.txt`


## Stage 4 — Publish and Verify Release Image

- Docker Hub repository: https://hub.docker.com/r/chahatup/fest-backend
- Published tags:
  - `chahatup/fest-backend:1.0.0`
  - `chahatup/fest-backend:1.0`
- Image digest: `sha256:764112d9759338ec8cfbc52a2d0f450712ec4acc27c8fb812256a98668065df7`
- Compose now uses the published `1.0.0` image.
- Verified the image could be pulled from Docker Hub and run.
- Health endpoint confirmed `database: true`, the required registration number, and version `1.0.0`.

