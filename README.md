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

There is an image in <https://hub.docker.com/repository/docker/exaesmwp4/containerized-jupyter-on-hpc> which you can use for the next steps.
 
## Running with Singularity

Once the image is built and with singularity in the path, run:
```shell
singularity run \
    -B $(mktemp -d):/run/user \
    --pwd /home/jovyan/ \
    docker://exaesmwp4/containerized-jupyter-on-hpc:latest
```

## Connect to Jupyter on a remote server

If `singularity` runs on a remote server and listens on a port that you cannot directly connect to (as is the default for HPC compute or frontend nodes), one possible solution is using an SSH tunnel to foward browser traffic.  Follow [this guide](https://git.geomar.de/python/jupyter_on_HPC_setup_guide#connect-to-jupyterlab-running-on-a-remote-machine) to learn how to do this.


(Note that you might want to replace `docker://exaesmwp4/containerized-jupyter-on-hpc:latest` with wherever you pushed the image.)
