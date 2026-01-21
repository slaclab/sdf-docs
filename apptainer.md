# Apptainer

For a detailed explanation of how to use Apptainer on SDF, you can go through Yee-Ting Li's presentation [here](https://confluence.slac.stanford.edu/display/AI/AI+Seminar#AISeminar-Containers!Containers!Containers!) where you can find both the slides and the zoom recording.

## Prerequisite

As pulling and building a new image can use quite a lot of disk space, we recommend that you set the appropriate cache paths for apptainer to not use your $HOME directory. Therefore, before pulling or building an image, define the following environment variables:

```bash
export DIR=${LSCRATCH}/.apptainer
mkdir -p $DIR
export APPTAINER_LOCALCACHEDIR=$DIR
export APPTAINER_CACHEDIR=$DIR
export APPTAINER_TMPDIR=$DIR
```

## Pulling images

To pull an image from DockerHub, do:
```bash
apptainer pull docker://<user or organization>/<repository>:<tag>
```

## Miscellaneous

By default apptainer overrides your terminal prompt with `Apptainer> ` in order to emphasize that you are opening a terminal within a container.
If you prefer a less stark reminder you may instead include the following lines in `~/.bashrc` for a more familiar prompt with a subtler `(apptainer)` prefix indicating the environment is within a container.
```bash
# add a prefix if this shell is in a container
export PROMPT_COMMAND='[ -f /singularity ] && PS1="(apptainer) ${PS1}"; unset PROMPT_COMMAND'
```
This would make the terminals that you open in Jupyter Lab appear with your customary prompt, except for the additional `(apptainer) ` prefix.
