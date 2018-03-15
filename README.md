# Docker Container for SlipStream Builds

This repository automates the creation of a Docker container for
SlipStream builds.  It contains all of the [external dependencies and
tools](http://ssdocs.sixsq.com/en/latest/developer_guide/dependencies.html)
required to build SlipStream.

## Running Container

The published container can be run with the command:

```
docker run -it sixsq/slipstream:build
```

By default, this starts a `bash` shell as root.  You can attach local
directories to the container to facilitate access to, for example, SSH
credentials or git workspaces.

Using the command:

```
docker run -it -v ~/.ssh:/root/.ssh sixsq/slipstream:build
```

will give access to your SSH configuration and credentials from within
the container.  You can have multiple `-v` options; other interesting
directories to share are your git workspaces and the local maven cache
`~/.m2`.

## Building Container

The build process uses maven and a Docker maven plugin to create the
container.  Just do the usual maven dance:

```
mvn clean install
```

to create a container locally (probably with changes to the dockerfile
commands).  This will put the container into your local Docker cache.
You can find the image with:

```
docker images
```

You should see something like the following listing:

```
sixsq/slipstream                                build                  ce92c494bb23        46 hours ago        691MB
sixsq/slipstream                                build-1.6.0-SNAPSHOT   ce92c494bb23        46 hours ago        691MB
```

Two tags will be published, the latest called "build" and the
versioned image "build-1.6.0-SNAPSHOT".  Note that these are
identical; Docker keeps only a single copy of the image under the
hood.

## Publishing Container

To publish the container, you must have an account on [Docker
Cloud](https://cloud.docker.com) and have been invited to the "sixsq"
organization.

Once you have access, you can then login to the Docker Cloud from the
command line:

```
$ docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username (clomps): 
Password: 
Login Succeeded
```

and then you can push images to the `sixsq/slipstream` repository with
the command `docker push`.

**Be sure to change the version number and to check in any
modifications.** Be careful not to overwrite existing contains with a
version.

## License

Copyright (c) 2018 SixSq Sàrl

DISTRIBUTED under the [Apache License, Version 2.0 (January
2004)](http://www.apache.org/licenses/LICENSE-2.0).
