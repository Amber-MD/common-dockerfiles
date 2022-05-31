# Common Dockerfiles

These Dockerfiles define build environments that run on [Jenkins](https://jenkins.jasonswails.com) to *build* popular MD packages.

Note that the [images](https://hub.docker.com/orgs/ambermd/repositories) created from these Dockerfiles *only* contain a working build environment for building Amber (they do *not* contain Amber itself). This represents the build environment used for the Amber (and OpenMM) CI builds on Jenkins for CPU and GPU builds both in serial and parallel.
