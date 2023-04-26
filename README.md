# CMS datatools
Singularity and docker containers for Tools for weather and climate data analysis tools.


##Details
Two containers are available, one for singularity/apptainer and one for Docker.
These provide a `conda` environment in which `cf-python`, `cf-plot`, `cfview`,
`esmvaltool` and `iris` are available.

##Usage
The containers are designed to be used via an interactive shell when started.
`esmvaltool` and `cfview` can be started via the command line, and `cf-python`,
`cf-plot` and `iris` are available within `python`.

##Singularity/apptainer.


###Setup for apptainer
If using `apptainer`, the SylabsCloud continer library needs to be configured.
This step isn't required for `singularity`.
```
$ apptainer remote add --no-login SylabsCloud cloud.sycloud.io
$ apptainer remote use SylabsCloud
```
then
```
$ apptainer remote list
```
should contain the lines (amoungs others)
```
NAME           URI                  ACTIVE  GLOBAL  EXCLUSIVE  INSECURE
SylabsCloud    cloud.sycloud.io     YES     NO      NO         NO
```
End of apptainer only section.

Now download the container:
```
$ singularity pull library://simonwncas/default/datatools
```
and run with
```
$ singularity shell -B /run datatools_latest.sif
```
##Docker.

The `docker` container is downloded with:

```
$ docker pull simonwncas/datatools
```
and started with
```
$ docker run -it simonwncas/datatools
```
note this will not mount any local disks.

If `cf-plot` or `cfview` are required, then extra options are needed for `Qt5` and `X11` graphics:
```
$ xhost + #allow the docker instance to access the local X11 server.
$ docker run -it -e "DISPLAY=$DISPLAY" -v "$HOME/.Xauthority:/root/.Xauthority:ro" --network host simonwncas/datatools
```
again, no local disks are mounted.

See https://medium.com/@mreichelt/how-to-show-x11-windows-within-docker-on-mac-50759f4b65cb for guidance on how to configure `docker` for `X11` on Macs.
