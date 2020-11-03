# Configuration and Launch

At this point you should have an executable binary for PhishDetect Node installed with all required dependencies.

You can now check the help message by launching:

```bash
phishdetect-node --help
```

This is the output that you should see:

    Usage of phishdetect-node:
          --api-version string    Specify which Docker API version to use (default "1.37")
          --brands string         Specify a folder containing YAML files with Brand specifications
          --contacts string       Specify a link to information or contacts details to be provided to your users
          --create-user           Create a new user
          --debug                 Enable debug logging
          --disable-analysis      Disable the ability to analyze links and pages
          --disable-api           Disable the API routes
          --disable-gui           Disable the Web GUI
          --disable-user-auth     Disable requirement of a valid user API key for all operations
          --host string           Specify the host to bind the service on (default "127.0.0.1")
          --mongo string          Specify the mongodb url (default "mongodb://localhost:27017")
          --port string           Specify which port number to bind the service on (default "7856")
          --safebrowsing string   Specify a file path containing your Google SafeBrowsing API key (default disabled)
          --yara string           Specify a path to a file or folder contaning Yara rules

## Command-line Parameters

### `--api-version`

Use this option to specify which API version for Docker you intend to use. In most cases you should be able to just ignore this option.

The default value is 1.37.

### `--brands`

Use this option to specify a path to a folder containing additional Brand definitions. These are used to extend the default [Brands](https://github.com/phishdetect/phishdetect/tree/master/brand) embedded in the core library. You can use this to create custom Brand definitions for your own domain names. Some additional custom brands are collected [here](https://github.com/phishdetect/phishdetect-extra-brands).

### `--contacts`

Use this option to specify a link to a separate webpage that provides additional information on your PhishDetect Node and perhaps your contact details.

### `--debug`

Use this option to enable debug-level logging. Beware that it is very verbose, so you might not want to turn this on in production.

### `--disable-analysis`

Use this option to disable the ability to perform dynamic analysis of suspicious links and web pages. This is the functionality that will make use of the Docker image. Using this option will turn off this functionality both on the Web GUI and on the REST API.

### `--disable-api`

Use this option to disable the REST API service. The REST API is used by the clients, such as the [browser extension](https://github.com/phishdetect/phishdetect-extension) to download lists of malicious indicators as well as to send alerts of suspected events to the PhishDetect Node administrator.

### `--disable-web`

Use this option to disable the Web GUI component of the service. The GUI is used by some clients, such as the browser extension, to request the dynamic analysis of suspicious links and pages.

### `--port`

Use this option to use a custom port number for the web server.

The default value is 7856.

### `--safebrowsing`

Use this option to provide your private API key for the Google Safebrowsing API.

*This functionality is currently experimental.*


## How to Launch

You should use the combination of options available that best suits your need. In most cases, you will simply have to make sure that MongoDB is installed and running and just launch PhishDetect Node with no arguments. This is what you should see:

    $ build/linux/phishdetect-node
    INFO[0000] Starting PhishDetect Node on 127.0.0.1:7856 and waiting for requests... 

As you can see, PhishDetect Node is now running on host 127.0.0.1 and port 7856. In order to make the service accessible to the public, you should configure an appropriate web server (such as Apache or nginx) and generate an SSL/TLS certificate for it.
