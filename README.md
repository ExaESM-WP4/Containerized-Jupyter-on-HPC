# Containerized Jupyter on HPC

Recipes for containerized execution of Jupyter on HPC.

## Dummy application

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/ExaESM-WP4/Containerized-Jupyter-on-HPC/master?filepath=example_application%2Fdata_analysis.ipynb)
This repo contains an [example application](example_application/data_analysis.ipynb).

## Build and push Docker image

We'll use [jupyter-repo2docker](https://repo2docker.readthedocs.io/) to build a docker image that is largely identical to the one used on <https://mybinder.org>, and push it to a registry (https://hub.docker.com/ for now).

With [Docker](https://docs.docker.com/install/) and with [jupyter-repo2docker](https://repo2docker.readthedocs.io/en/latest/install.html) installed, run
```shell
jupyter-repo2docker \
   --image-name <image-name> \
   --user-name jovyan \
   --push \
   --no-run \
   https://github.com/ExaESM-WP4/Containerized-Jupyter-on-HPC
```
picking an image name.
 
