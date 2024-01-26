---
description: >-
  This page explains the various wallet options available for Joystream and how
  to use them.
---

# 💳 Wallets

Joystream is an independent Layer 1 blockchain and although it uses the same framework as Polkadot called Substrate, it is not a Polkadot Parachain and you cannot send Joystream tokens to Polkadot addresses--please be careful to not send Joystream's token to exchanges or wallets that do not support Joystream

You can use any of the below wallets to connect to Polkadot Vault which will allow you to use a dedicated smartphone as an airgapped signer. It is highly recommended to store your assets using this as it is the most secure option available. Nova

<table><thead><tr><th>Wallet</th><th width="199.33333333333331">Description</th><th>Notes</th></tr></thead><tbody><tr><td><a href="https://www.talisman.xyz">Talisman</a></td><td><em>Keep your assets safe, manage your portfolio and explore Polkadot and Ethereum apps with Talisman</em></td><td><ul><li>Browser Extension available</li><li>Supports Polkadot Vault</li><li>Dashboard where you can see your balances and other information</li></ul></td></tr><tr><td><a href="https://novawallet.io">Nova</a></td><td>Next gen wallet for Dotsama ecosystem.</td><td><ul><li>Supports hardware wallets</li><li>65+ networks supported</li></ul></td></tr><tr><td><a href="https://www.subwallet.app">Subwallet</a></td><td><em>Comprehensive Polkadot,Substrate &#x26; Ethereum wallet</em></td><td><ul><li>Browser &#x26; Mobile wallets available</li><li>Supports Polkadot Vault</li><li>Dashboard where you can see your balances and other information</li></ul></td></tr><tr><td><a href="https://onekey.so">OneKey</a></td><td>Open source crypto wallet. Trusted by millions.</td><td><ul><li>Hardware and software wallet</li></ul></td></tr><tr><td><a href="https://signer.parity.io">Polkadot Vault</a></td><td><em>Turn your extra phone, tablet, or any other iOS or Android device into a hardware wallet.</em></td><td></td></tr></tbody></table>

## Polkadot Vault Tutorial

Joystream supports Polkadot Vault which enables users to utilize almost any smartphone or table to store their accounts in a secure and convenient way. The smartphone used should, once setup, never connect to the internet again and be dedicated for this purpose. QR codes are used to ensure the device remains airgapped.

**Requirements:**

* [A wallet that supports Joystream](wallets.md) (such as Subwallet, Talisman or Polkadot-js Extension)
* A dedicated smartphone (which can be an older model) to store the accounts. Note that the camera quality of the device needs to be capable of scanning a quite complex QR code, so the device should preferably not be too old.
* A webcam on your computer

#### Basic setup

1. Set up Polkadot Vault
   1. Install the [Polkadot Vault](https://signer.parity.io/) app on your phone.
   2. Disconnect your phone from the internet forever. Best to remove any SIM cards, forget any WiFi network, enable airplane mode, etc.
2. Add Joystream network to Polkadot Vault
   1. On your computer, open the [Joystream Metadata Portal](https://metadata.joyutils.org/) that will allow you to add Joystream as a network in Vault.
   2. Select Joystream network on the left menu
   3. Now select “Chain Specs” tab.\
      ![](<.gitbook/assets/image (1).png>)
   4. In the Polkadot Vault smartphone app, press `scanner` at the bottom of the screen and scan the chain spec QR from Metadata Portal.\
      ![](<.gitbook/assets/image (4).png>)
   5. Now approve the Joystream network\
      ![](.gitbook/assets/vault\_approve\_app\_ws.jpeg)
   6. Now press `Add Network Metadata`\
      ![](.gitbook/assets/vault\_add\_metadata.jpeg)
   7. Once done, click `Metadata` on the Metadata portal do the same for chain metadata (“Metadata” tab on the right). This is multi-part QR so you need to keep your camera on the animated QR until the scan is completed. On devices with low camera quality, it can even take few minutes.\
      ![](<.gitbook/assets/image (3).png>)
   8. Now click `Approve` to approve the network metadata\
      ![](.gitbook/assets/vault\_Approve\_metadata\_ws.jpeg)
3. Generate/import your keys into Vault. This is done in “Key Sets” tab in Vault. If you are generating new keys, make sure to securely back up your seed phrase. To keep the air-gap, you should never keep your seed phrase on an online device. Old pen and paper are your best friends. When adding a key, make sure to select Joystream as network for it.
4. Set up your desktop extension. You can use both SubWallet and Talisman extensions. For this example, we’ll use SubWallet.
   1. Install SubWallet browser extension
   2. During setup, select “Attach an account” and click “Connect a Polkadot Vault account".\
      ![](.gitbook/assets/extension\_subwallet\_attach\_polkadot\_option.png)\\
   3. Click “Scan QR code”. This will most likely fail because of no camera access. Click the “Go to Settings” button and toggle “Camera access for QR” at the bottom. At this point you will most likely also need to allow camera access in browser/system popup.
   4. Once done, click back button in top left corner. You should now see preview from your camera.
   5. In the Polkadot Vault app, on “Key Sets” tab, select your keypair. Then, select the account from your keypair you want to use (you can derive multiple accounts from a single keypair). You should now see QR code with your public key. Place your phone in front of your desktop camera to finish SubWallet import
   6. At this point your account is imported into SubWallet. To finish the setup, you may want to enable Joystream network balance in SubWallet. To do so, click settings icon in top right corner and enable Joystream in the list of networks.
5. Now that your account is imported, you can use it as you would any other.
   1. Connect your SubWallet extension to Pioneer/Atlas/Gleev
   2. When you want to send a transaction, you will be presented with a QR code. Scan it with your Vault.
   3. Vault will produce another QR that represents this signed transaction. Scan it back on your desktop.
6. All done!

_(A special thanks to Klaudiusz for writing this tutorial and also setting up the metadata portal)_
