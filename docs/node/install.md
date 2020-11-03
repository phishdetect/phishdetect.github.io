# Install PhishDetect Node

Before installing and launching PhishDetect Node you are required to install some dependencies. 

## Install MongoDB

First and foremost, you will need to install [MongoDB](https://www.mongodb.org) which is used by PhishDetect Node for data storage. All of the configuration, alerts, reports, and indicators will be stored in a `phishdetect` database on a locally running MongoDB instance. Please refer to the [official documentation](https://docs.mongodb.com/manual/installation/) for instructions on how to install MongoDB on your Linux distribution of choice.

## Install Yara

For the proper functioning of PhishDetect Node, you will also need to install [Yara](https://virustotal.github.io/yara/). Although Yara might come packaged in your Linux distribution, it is preferable that you compile it from sources. You should refer to the official documentation for more details, but the installation process should be more or less the following:

```bash
sudo apt-get update -qq
sudo apt-get install automake libtool make gcc pkg-config
wget https://github.com/VirusTotal/yara/archive/v4.0.1.tar.gz
tar -zxf v4.0.1.tar.gz
cd yara-4.0.1
"./bootstrap.sh"
"./configure"
make
sudo make install
sudo ldconfig
```

## Install Docker

PhishDetect Node is capable of conducting dynamic analysis of suspicious URLs by opening them through a Google Chrome browser running in a disposable [Docker](https://www.docker.com/) container. In order to leverage this functionality, which can be [optionally disabled](run.md), you necessarily have to install Docker and PhishDetect's docker image.

You should refer to Docker's [official documentation](https://docs.docker.com/engine/install/) for instructions on how to install it on your Linux distribution of choice. However **please note**: in order to minimize any potential security risks involved in exposing a Docker service, you should considering installing and launching Docker in [rootless mode](https://docs.docker.com/engine/security/rootless/). Through this configuration Docker is launched with regular user privileges instead of root, mitigating potential vulnerabilities in the daemon and the container runtime.

Once you have your Docker daemon installed and running, you can proceed downloading PhishDetect's Docker image (make sure you are running this command from the same user you intend to launch PhishDetect Node's binary from):

```bash
docker pull phishdetect/phishdetect
```

If everything worked fine, the command `docker images` should return an output similar to this:

    REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
    phishdetect/phishdetect   latest              dcda88861ad6        3 months ago        1.63GB


## Install PhishDetect Node

At this point you will only need to run the `phishdetect-node` binary. If you decided to compile it by yourself from sources, you should upload the binary from the build system to your server.

Otherwise, you can simply download a pre-compiled binary which is made available for every PhishDetect Node release. [Here](https://github.com/phishdetect/phishdetect-node/releases/latest) you find the most recent version. Download the distributed binary directly on your server for example with:

```bash
wget https://github.com/phishdetect/phishdetect-node/releases/download/v2.9.2/phishdetect-node
```

Now make sure to set the binary as executable:

```bash
chmod +x phishdetect-node
```

In the [next section](run.md) you will find details on how to launch PhishDetect Node and an explanation of all available command-line arguments.

## Optional: Install a Webserver

By default, when executed, PhishDetect Node will run on `localhost` and port `7856`. In order to enable a secure TLS-encrypted service, and to properly handling connections and optional logging, you should install your preferred webserver and configure it to proxy requests to the local address PhishDetect Node is running on. This documentation provides instructions on how to do so using [Nginx](nginx.md).
