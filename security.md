---
description: Security related resources and information.
---

# 🔐 Security

## Vulnerability Reporting

To report issues in a responsible manner, please send to "<mark style="color:red;">**security" on domain "joystream.org"**</mark>, and encrypt the message, this is however _**not**_ a support channel.

Your report should include the following:

* your name
* description of the vulnerability
* attack scenario (if any)
* components
* reproduction
* other details

Try to include as much information in your report as you can, including a description of the vulnerability, its potential impact, and steps for reproducing it. Be sure to use a descriptive subject line.

You'll receive a response to your email within 5 business days indicating the next steps in handling your report. We encourage finders to use encrypted communication channels to protect the confidentiality of vulnerability reports. You can encrypt your report using our public key.&#x20;

After the initial reply to your report, our team will endeavor to keep you informed of the progress being made towards a fix. These updates will be sent at least every five business days.

Thank you for taking the time to responsibly disclose any vulnerabilities you find.

### Responsible Investigation and Reporting

Responsible investigation and reporting includes, but isn't limited to, the following:

* Don't violate the privacy of other users, destroy data, etc.
* Don’t defraud or harm Parity Technologies Ltd or its users during your research; you should make a good faith effort to not interrupt or degrade our services.
* Don't target our physical security measures, or attempt to use social engineering, spam, distributed denial of service (DDOS) attacks, etc.
* Initially report the bug only to us and not to anyone else.
* Give us a reasonable amount of time to fix the bug before disclosing it to anyone else, and give us adequate written warning before disclosing it to anyone else.
* In general, please investigate and report bugs in a way that makes a reasonable, good faith effort not to be disruptive or harmful to us or our users. Otherwise your actions might be interpreted as an attack rather than an effort to be helpful.

## Secure Communication

The following GPG keys may be used to communicate sensitive information to relevant developers, in particular concerning the runtime and blockchain, but also other critical infrastructure and applications. These recipients will relay the message securely to whomever is the maintainer at any given time.

<table><thead><tr><th width="184">Joystream Hande</th><th>Fingerprint</th></tr></thead><tbody><tr><td><code>mokhtar</code></td><td><code>2DD5D822FC22DB196E262440ADA7C97DDD6781D8</code></td></tr></tbody></table>

You can import a key by running the following command with that individual’s fingerprint: `gpg --keyserver hkps://keys.openpgp.org --recv-keys "<fingerprint>"` Ensure that you put quotes around fingerprints containing spaces.

## Security Audits

Two runtime audits have been conducted so far

* **Quarkslab:** [https://github.com/Joystream/audits/tree/main/Quarkslab-22-05-982-REP](https://github.com/Joystream/audits/tree/main/Quarkslab-22-05-982-REP)
* **SRLabs:** [https://github.com/Joystream/audits/tree/main/SRL-Jsgenesis\_baseline\_security\_assurance\_joystream-2021](https://github.com/Joystream/audits/tree/main/SRL-Jsgenesis\_baseline\_security\_assurance\_joystream-2021)
