# Dockerfiles Repository

This repository contains various Dockerfiles for different development environments and build configurations.

## Available Docker Images

- `fluidsynth-devel` - FluidSynth development environment on openSUSE Leap
- `qt6-dbg.suse` - Qt6 debug environment on openSUSE with debug symbols
- `qt6-kf6.ubuntu` - Qt6 with KDE Framework on Ubuntu
- `qt6.suse` - Qt6 development environment on openSUSE
- `qt6.ubuntu` - Qt6 development environment on Ubuntu
- `qt6.win` - Qt6 development environment for Windows with vcpkg dependencies

## Automated Docker Image Building

This repository includes a GitHub Actions workflow that automatically builds Docker images when Dockerfiles are modified. The workflow:

- ✅ Only runs when Dockerfile directories or dependencies are changed
- ✅ Detects which specific Dockerfiles have been modified
- ✅ Builds only the changed Docker images (efficient resource usage)
- ✅ Tags images with the commit SHA for version tracking
- ✅ Pushes to a configurable container registry

### Configuration

To configure the Docker registry and credentials, set these repository variables and secrets:

**Variables (Repository Settings → Secrets and variables → Actions → Variables):**
- `DOCKER_REGISTRY` - Registry URL (defaults to `ghcr.io`)
- `DOCKER_USERNAME` - Registry username (defaults to GitHub actor)

**Secrets (Repository Settings → Secrets and variables → Actions → Secrets):**
- `DOCKER_PASSWORD` - Registry password/token (required)

### Image Tagging

Built images are tagged with:
- Branch name (for branch pushes)
- PR number (for pull requests)
- Commit SHA (always included)

Example tags:
- `ghcr.io/owner/fluidsynth-devel:main-abc1234`
- `ghcr.io/owner/qt6.ubuntu:abc1234567890abcdef1234567890abcdef123456`

### Special Dependencies

- The `qt6.win` image depends on certificates in the `certs/` directory
- When certificates are updated, `qt6.win` will be automatically rebuilt
- Other Dockerfiles are independent and only rebuild when their specific file changes