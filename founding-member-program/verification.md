---
description: How to start the KYC process after reaching the induction threshold.
---

# Verification

## Read This First!

<mark style="color:red;">We are receiving a lot of emails, so don't expect a reply right away. Going forward, we will contact you within 1 week IF:</mark>

* <mark style="color:red;">Your verification is accepted -> you will be prompted for the next step(s)</mark>
* <mark style="color:red;">Your verification failed (bad signature, missing info, etc.) -> you will be told to send again</mark>

If you send an email to get verified, despite not having reached the threshold, thus not listed under [inductions.md](inductions.md "mention") , you will **NOT** receive a reply whether you failed or not.&#x20;

## FAQ

* Q: "I am close, and expect to reach the Threshold after grading of next round. Should I send an email".
  * A: **No. The email will likely get deleted, forcing you to send again.**

## Email

To get the KYC process started, send an email to `founding.members-at-jsgenesis.com`, with the subject **`FM Induction - <myMemberId>`**

The email itself must contain a specific message, in the format below:

```
I am <name> born <year> with Member ID <myMemberId>.
Secure contact info:
Email: <myEmail>
Discord: <mydiscord#1337>
<contactPlatform>: <platformId>
```

Whereas Email and Discord are mandatory, you may _optionally_ add keybase, telegram or signal.&#x20;

Note that the email must be the same as you are sending from, and that it will be our default way of reaching you for "official" matters. The others are fallback solutions.

### Sign Message

The message above must be signed with your membership root or controller key in order for us to ensure you control the keys of the membership. Steps:

1. Go to [polkadot-js](https://polkadot.js.org/apps/#/signing) -> `developer` -> `Sign message` and select your membership root or controller key.
2. Paste in the **exact** message (if not, the signature verification will fail), and click "Sign message"
3. Copy the "signature of supplied data" and paste it in the email.

Send the email, and we will get back to you with further instructions.

If you don't want to send this information in cleartext, feel free to encrypt your message with [this pgp key](https://keys.openpgp.org/search?q=founding.members%40jsgenesis.com).&#x20;

### Example

Message

```
I am John Doe born 1901 with Member ID 9999.
Secure contact info:
Email: john@doe.com
Discord: johnnydoey#1337
```

Signing

![Signed message](<../../.gitbook/assets/Screen Shot 2022-08-22 at 00.53.22.png>)

The returned signature...

`0x0e0bdd3abc487a466e740b2c1fec96a215b1f6f631f9d68cb2d5ea4b7b78c246212ce40dac883a4aabe479468d296221250b1c3152d015425fc772efae703786`

...can then be verified against the address `5DaDUnNVzZPwK9KLwyPFgeSbc9Xeh6G39A2oq36tiV9aEzcx`.

![](<../../.gitbook/assets/Screen Shot 2022-08-22 at 00.52.37.png>)

