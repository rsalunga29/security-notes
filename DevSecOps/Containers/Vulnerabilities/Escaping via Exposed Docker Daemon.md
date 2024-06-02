Containers interact with the host operating system using the Docker Engine (and, therefore, have access to the Docker socket!) This socket (named `docker.sock`) will be mounted in the container. The location of this varies by the operating system the container is running, so you would want to `find` it. If the container runs Ubuntu 18.04, the `docker.sock` is located in `/var/run`.

First we must confirm if we can execute docker commands using the `groups` command as a low-privileged user. Alternatively, you must be root.
```
We will use Docker to create a new container and mount the host's filesystem into this new container. Then we are going to access the new container and look at the host's filesystem.

Our final command will look like this: `docker run -v /:/mnt --rm -it alpine chroot /mnt sh`, which does the following:

1. We will need to upload a docker image. For this room, I have provided this on the VM. It is called "alpine". The "alpine" distribution is not a necessity, but it is extremely lightweight and will blend in a lot better. To avoid detection, it is best to use an image that is already present in the system, otherwise, you will have to upload this yourself.

2. We will use `docker run` to start the new container and mount the host's file system (/) to (/mnt) in the new container: `docker run -v /:/mnt` 

3. We will tell the container to run interactively (so that we can execute commands in the new container): `-it`

4. Now, we will use the already provided alpine image: `alpine`

5. We will use `chroot` to change the root directory of the container to be _/mnt_ (where we are mounting the files from the host operating system): `chroot /mnt`

6. Now, we will tell the container to run `sh` to gain a shell and execute commands in the container: `sh`
```