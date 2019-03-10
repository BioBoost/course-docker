# Chapter 04 - Running Containers

Running images with Docker can be done using the `docker run` command. The command can take many attributes that supply information on how to run the container. It also allow you to override all defaults set by the image developer, as well as those set by the docker runtime.

To run the well-known `hello-world` image, we can use the following command.

```bash
docker run hello-world:latest
```

Here `hello-world` is the name of the image and `latest` is the version tag, which allows you to pick a specific version to run a container from.

This will pull the latest image from Docker Hub and spawn a container from it. The container will execute the binary which generates the output. This output is then redirected via the Docker client to your current terminal.

> **INFO** - **Docker Hub**
>
> Sharing Docker images is made easy by Docker Hub. Anybody can create an account on Docker Hub to distribute images that can be deployed on other systems or by other users. Therefore it will always be the first place we'll check if someone did not do most of the work for us.