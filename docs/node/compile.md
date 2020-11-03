# Compile from sources

This page contains instructions on how to compile PhishDetect Node from sources. Pre-compiled binaries for PhishDetect Node are already made available through [GitHub Releases](https://github.com/phishdetect/phishdetect-node/releases). If you wish to use our pre-compiled binaries you can skip this section and move to the [installation instructions](install.md).

## Install all the build tools

If you decided to build your own binary from the PhishDetect Node source code, you will need to have a working **Go 1.14+** environment configured. Please refer to the official documentation on how to install the most recent version of Go on your system of choice. If your system doesn't provide binary packages for recent versions of Go you might have to build Go from sources as well (in that case, you might want to consider using something like [GVM](https://github.com/moovweb/gvm)). If so, keep in mind you might need some minimum requirements, such as at least 1GB of memory.

It is critically important for the successful compilation of PhishDetect Node that you have `$GOPATH` properly set, and for the `$GOPATH/bin/` folder to be added to your `$PATH` environment varilable. You should configure this in your `.bashrc` or `.zshrc` file like following:

```bash
export $GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```

Now you should install the required build tools. On Debian/Ubuntu systems you can do so like following:

```bash
sudo apt install pkg-config git make
```

## Install Yara

In order to build a PhishDetect Node binary you will also need to install [Yara](https://virustotal.github.io/yara/). Although Yara might come packaged in your Linux distribution, it is preferable that you compile it from sources. You should refer to the official documentation for more details, but the installation process should be more or less the following:

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

PhishDetect Node uses Yara to optionally scan suspicious pages with provided Yara rules. Despite this being an optional functionality, compiling PhishDetect Node from sources nevertheless requires libyara being installed on the build system.

Ideally you should compile your PhishDetect Node with the same Yara version you will eventually install on the production server the Node will run on.

## Compile the binary

At this point, you should have a working Go build system. You can now clone PhishDetect Node's git repository:

```bash
git clone https://github.com/phishdetect/phishdetect-node.git
```

Move into the newly created folder:

```bash
cd phishdetect-node
```

To build the binary you can simply launch the `make` command. This will attempt to download all required Go dependencies and additional tools, and finally compile PhishDetect Node.

If it completed successfully, you should find a compiled binary called `phishdetect-node` inside the `build/` folder. This binary is all you need to run the PhishDetect Node service.

You can now move on to the [next section](install.md) for instructions on how to set PhishDetect Node up on your production server.
