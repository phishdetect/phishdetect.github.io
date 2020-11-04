# Configuration and Launch

At this point you should have an executable binary for PhishDetect Node installed with all required dependencies. You can now check available command-line parameters using `--help`:

```bash
./phishdetect-node --help
```

Which should result in the following:

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

## Create an Administrator

As a first step you should create your own Administrator account through the following command:

```bash
./phishdetect-node --create-user
```

You will be offered a step-by-step process through which you will be able to select the account's trust level, specify a user name and an email address. At the end, you should be provided with a REST API key. Note down this key, you will need it later.

## Launch PhishDetect Node

Launching PhishDetect Node is as simple as launching this command:

```bash
./phishdetect-node
```

You should see something similar to the following:

    INFO[2020-11-03 13:33:37 +0100] Enable API: true                             
    INFO[2020-11-03 13:33:37 +0100] Enable GUI: true                             
    INFO[2020-11-03 13:33:37 +0100] Enable Analysis: true                        
    INFO[2020-11-03 13:33:37 +0100] Enforce User Auth: true                      
    INFO[2020-11-03 13:33:37 +0100] Starting PhishDetect Node on 127.0.0.1:7856 and waiting for requests... 

Without specifying any additional command-line parameters, PhishDetect Node is launched with the following configuration:

1. Enable REST API routes.
2. Enable GUI pages such as registration form, and link analysis.
3. Enable dynamic analysis through the Dockerized Chrome browsers.
4. Enforce user authentication, and require new users to register and be activated.
5. Launch PhishDetect Node on host `127.0.0.1` and port `7856`.

All of these settings can be changed through the appropriate command-line parameters.

## Command-line Parameters

### `--api-version`

Use this option to specify which API version for Docker you intend to use. In most cases you should be able to just ignore this option.

The default value is 1.37.

### `--brands`

Use this option to specify a path to a folder containing additional Brand definitions. These are used to extend the default [brands](https://godoc.org/github.com/phishdetect/phishdetect/brand#Brand) embedded in the core library. You can use this to create custom Brand definitions for your own domain names. Custom brand defintions should come in the following YaML format and stored with `.yaml` or `.yml` file extensions:

```yaml
name: google
original:
    - google
    - gmail
safelist:
    - google.com
    - google.de
    - google.it
    - google.fr
suspicious:
    - goooogle
    - goolge
```

`name` should contain the name of the brand. `original` should contain words associated with the particular brand, including for example product names. `safelist` should contain a list of legitimate domain names associated with the brand. `suspicious` should contain a list of suspicious permutations of the original brand names which will be used to determine if a suspicious domain or URL is attempting to spoof this particular brand.

### `--contacts`

Use this option to specify a link to a separate webpage that provides additional information on your PhishDetect Node and perhaps your contact details.

### `--create-user`

Use this command-line parameter to follow a step-by-step process to create a new user account and obtain its API key.

### `--debug`

Use this option to enable debug-level logging. Beware that it is very verbose, so you might not want to turn this on in production.

### `--disable-analysis`

Use this option to disable the ability to perform dynamic analysis of suspicious links and web pages. This is the functionality that will make use of the Docker image. Using this option will turn off this functionality both on the Web GUI and on the REST API.

### `--disable-api`

Use this option to disable the REST API service. The REST API is used by the clients, such as the [browser extension](https://github.com/phishdetect/phishdetect-extension) to download lists of malicious indicators as well as to send alerts of suspected events to the PhishDetect Node administrator.

### `--disable-gui`

Use this option to disable the Web GUI component of the service. The GUI is used by some clients, such as the browser extension, to request the dynamic analysis of suspicious links and pages.

### `--disable-user-auth`

Use this option to disable the enforcement of user authentication. Users will be able to configure their clients, such as the browser extension, to use your Node without having to register and without having to provide a valid API key.

### `--host`

Specify the host to bind PhishDetect Node on.

The default value is `127.0.0.1`.

### `--mongo`

Specify a custom connection string to MongoDB.

The default value is `mongodb://localhost:27017`.

### `--port`

Use this option to use a custom port number for the web server.

The default value is `7856`.

### `--safebrowsing`

Use this option to provide your private API key for the Google Safebrowsing API.

*This functionality is currently experimental.*

### `--yara`

Use this option to specify a path to a file or a folder containing Yara rules. Upon launch, PhishDetect Node will find and load all Yara rules contained at this path and subsequently use them for the analysis of suspicious HTML pages and for the dynamic analysis of suspicious links.
