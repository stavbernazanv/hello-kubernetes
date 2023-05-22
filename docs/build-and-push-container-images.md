# Build and push container images

The `hello-kubernetes` container image can be built and pushed to your own registry or or DockerHub repository. Currently only the `linux/amd64` architecture is supported.

## Prerequisites

- [make](https://www.gnu.org/software/make/)
- [Docker cli](https://www.docker.com/)
- Container registry

If you are using the [VS Code Remote Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) based development environment, all of the prerequisites will be available in the terminal.

## Makefile configuration

The `Makefile` in the root folder of the repo provides the functionality to allow you to build and push your own `hello-kubernetes` container image.

### Environment variables

| Name | Default | Description | 
| ---- | ------- | ----------- |
| REGISTRY | docker.io | The container registry to push the images to. |
| REPOSITORY | bernaz7 | The repository (or hierarchy) within the container registry where the image will be located. |
| IMAGE_VERSION | the version in src/app/package.json | The image version (label) to use for the built and pushed container images. |

### Targets

| Name | Description |
| ---- | ----------- |
| build-image-linux | Build the `hello-kubernetes` container image for the `linux/amd64` architecture. |
| push-image | Push the `hello-kubernetes` container image to the defined registry. |

## Building a container image

You can build the `hello-kubernete` container image as follows:

```bash
# Build the bernaz7/hello-kubernetes:$version image
make build-image-linux

# Build the bernaz7.azurecr.io/bernaz7/hello-kubernetes:$version image
export REGISTRY=bernaz7.azurecr.io
make build-image-linux
```

## Pushing a container image

You can push your built `hello-kubernetes` container image to the defined registry as follows:

```bash
# Push bernaz7/hello-kubernetes:$version to docker hub.
# Will tag $majorversion and $majorversion.$minorversion.
#
# Example: The container image will be tagged as follows for $version=1.10.0
#   - bernaz7/hello-kubernetes:1.10.0
#   - bernaz7/hello-kubernetes:1.10
#   - bernaz7/hello-kubernetes:1
make push-image

# REGISTRY=bernaz7.azurecr.io
# Push bernaz7.azurecr.io/bernaz7/hello-kubernetes:$version to bernaz7.azurecr.io.
# Will tag $majorversion and $majorversion.$minorversion.
#
# Example: The container image will be tagged as follows for $version=1.10.0
#   - bernaz7.azurecr.io/bernaz7/hello-kubernetes:1.10.0
#   - bernaz7.azurecr.io/bernaz7/hello-kubernetes:1.10
#   - bernaz7.azurecr.io/bernaz7/hello-kubernetes:1
export REGISTRY=bernaz7.azurecr.io
make push-image
```