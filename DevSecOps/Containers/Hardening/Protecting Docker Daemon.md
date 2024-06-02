Docker daemon is responsible for processing requests such as managing containers and pulling or uploading images to a Docker registry. Docker can be managed remotely and is often done in CI (Continuous Integration) and CD (Continuous Development) pipelines.

If an attacker can interact with the Docker daemon, they can interact with the containers and images. For example, they launch their own (malicious) containers or gain access to containers running applications with sensitive information (such as databases).

The Docker daemon is not exposed to the network by default and must be manually configured. However, exposing the Docker daemon is a common practice (especially in cloud environments such as CI/CD pipelines).
## SSH
Developers can interact with other devices running Docker using SSH authentication. To do so, Docker uses contexts which can be thought of as profiles. These profiles allow developers to save and swap between configurations for other devices.

To create Docker context, we can use the following command:
```bash
docker context create --docker host=ssh://myuser@remotehost --description="dev env" dev-env-host
```

Once this has been completed, you can switch to this context, where all Docker-related commands will now be executed on the remote host.
```bash
docker context use dev-env-host
```
> Note: This is not entirely secure. For example, a weak SSH password can lead to an attacker being able to authenticate. Strong password hygiene is strongly recommended.
## TLS Encryption
The Docker daemon can also be interacted with using HTTP/S. This is useful if, for example, a web service or application is going to interact with Docker on a remote device.

To do this securely, we can use the TLS protocol to encrypt the data sent between the devices. When configured in TLS mode, Docker will only accept remote commands from devices that have been signed against the device you wish to execute Docker commands remotely.

On the host (server) that you are issuing the commands from:
```bash
dockerd --tlsverify --tlscacert=myca.pem --tlscert=myserver-cert.pem --tlskey=myserver-key.pem -H=0.0.0.0:2376
```

On the host (client) that you are issuing the commands from:
```bash
docker --tlsverify --tlscacert=myca.pem --tlscert=client-cert.pem --tlskey=client-key.pem -H=SERVERIP:2376 info
```
> Note: It is important to remember that this is not guaranteed to be secure. For example, anyone with a valid certificate and private key can be a "trusted" device.