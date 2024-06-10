Unfortunately, there are numerous examples of malicious Docker images causing havoc. For instance, in 2020, Palo Alto discovered [cryptomining Docker images](https://unit42.paloaltonetworks.com/cryptojacking-docker-images-for-mining-monero/) that were pulled (and presumably ran) over two million times. Thus, it is important to review Docker images before using them.

Images on Docker Hub often come with the Dockerfiles attached to the repository, allowing you to view the different layers. Additionally, some images will often include open-source code repositories, allowing you to review the entirely of a Dockerfile, allowing us to audit the code and understand precisely what actions are being executed in the container.

Tools such as [Dive](https://github.com/wagoodman/dive) allow you to reverse engineer Docker images by inspecting what is executed and changed at each layer of the image during the build process.