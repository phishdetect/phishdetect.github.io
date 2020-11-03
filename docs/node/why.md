# Why to run a node?

A **PhishDetect Node** is a server running a PhishDetect service, offering the web interface and the REST API that PhishDetect clients, such as the [browser extension](https://github.com/phishdetect/phishdetect-extension) and others, can interact with.

For example, by default the extension is configured to use a PhishDetect Node located at **phishdetect.securitywithoutborders.org** that is operated by the cretors of PhishDetect and [Security Without Borders](https://www.securitywithoutborders.org). However, we encourage the creation of independent Phishdetect Nodes whenever possible.

There are multiple reasons why you would want to setup your own PhishDetect Node.

## Avoid blocklists

While there might be several ways for an attacker to identify a PhishDetect Node connecting to the phishing kits (for example by fingerprinting the instrumented headless Google Chrome browser), the most obvious way is by blocklisting the originating IP address. Because the default Node is publicly accessible and is not meant to be resistant to fingerprinting, it might be the case that careful attackers might notice it and block it. By running your own PhishDetect Node you will be able to diversify and reduce the risk of getting blocklisted.

## Enforce your own privacy policy

While we do the best to protect users' privacy, you might want to run your own PhishDetect Node to reduce exposure of potential personal or private information (see our [Privacy Policy](https://phishdetect.io/help/privacy/) for more details on what data could be collected).

## Maintain visibility on your users

If you work for an organization or are part of a group of people who might benefit from using PhishDetect, you might want to run your own Node in order to more directly support your peers and have some visibility over the suspicious links they might receive. Because PhishDetect is free software, you can also modify to better suit yours or your organization's needs and perhaps integrate it in other existing workflows and processes.

## Distribute your own private indicators

A PhishDetect Node can offer a list of hashed known bad indicators, such as bad email addresses and bad domains. These indicators can be used by the clients to monitor and block any known bad content. By running your own PhishDetect Node you will be able to distribute your own private indicators to your users.
