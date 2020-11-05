# Concept & Design Principles

PhishDetect is a suite of libraries and tools to assist with the reporting, detection and prevention of phishing and other forms of digital attacks. As mentioned, PhishDetect was conceived to fill gaps in civil society's cyber security ecosystem, and aiding the efforts of non-profits supporting human rights defenders and journalists. The lack of availability of security products and services to this segment of society, which is nevertheless highly targeted by cyberattacks, demands reinventing some wheels in order to better cater to the highly underfunded, diverse and distributed technological ecosystem typical of civil society.

While PhishDetect developers do not discourage the adoption of our software for other use-case scenarios, the development continues in respect of the following concepts and design principles that went into PhishDetect's creation.

## Designed for At-Risk End-Users

PhishDetect's primary goal is to facilitate the adoption of security protocols by at-risk end-users, who often work independently, with personal hardware and software, and without the support of a dedicated IT department.

## Consent-based Information Sharing

While granting remote control of accounts or devices to PhishDetect operators would be much simpler and possibly enable more effective monitoring for any suspicious activity, it would be ethically questionable and constitute a liability. We do not want to centralise excessive powers in the hands of PhishDetect operators, especially if that could lead to further compromise of at-risk users. Particularly because of heightened risks, PhishDetect's end-users should retain as much control as possible.

Therefore PhishDetect, and any of its official client applications, shall never grant developers or operators access to any user's device or account.

Any automated alerts from official PhishDetect client applications (such as the [Browser Extension](https://github.com/phishdetect/phishdetect-extension)) can only contain metadata, and not the content of any communication (for example the content of emails or web pages), and only be pertinent to known-malicious activity. Additionally, users should be allowed to optionally disable all automated alerts, if they decide to do so.

Any reporting of communications content, such as full-source emails, or of undetected activity, such as URLs the user suspects to be malicious, can only happen with the explicit consent and manual approval of the end-user.

## Collective Participation Equals Collective Protection

End-users shouldn't only be passive recipient of a service, but they should be incentivized to actively engage. A core part of PhishDetect's design is to simplify users' reporting of suspicious emails and links. Active users' participation in the detection and reporting of suspected attacks results in the collective protection of all others.

Through PhishDetect, a targeted user can report suspected malicious emails or links, operators can verify them and immediately issue new indicators of compromise, which all other users will shortly after automatically fetch. In a matter of minutes, a single PhishDetect user contributes protecting everyone else. Collective participation therefore equals collective protection.
