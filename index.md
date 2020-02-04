---
layout: default
title: 1. Overview
nav_order: 1
summary: A step-by-step protocol for companies to securely store bitcoin investments without the need for a third-party custodian.
image: /assets/cerberus_title.png
---

IMPORTANT: This protocol is under development and not yet ready for use.
{: .label .label-red }

Overview
========

![The Cerberus Protocol](/assets/cerberus_title.png)

## Introduction

The Cerberus Protocol is a step-by-step protocol for **companies** to securely store **bitcoin investments** without the need for a third-party custodian.

The protocol combines both *technical* and *procedural* guidance for bitcoin storage:
- **Technical:** Open source bitcoin hardware and software recommendations to securely distribute control, ensuring no single point of failure.
- **Procedural:** Policies to ensure that any incoming or outgoing transactions are conducted under strict checks and balances.

Cerberus is a fully open source protocol, authored and reviewed by bitcoin industry veterans, taking inspiration from excellent open-source work such as the [Glacier Protocol](https://glacierprotocol.org/).

### Cerberus is intended for:
* **Companies:** The bitcoin are owned by a collective entity rather than a single individual. Usually this will be an incorporated company.
* **Bitcoin investments:** Long-term bitcoin storage with a low transaction frequency (a handful of transactions per month).
* **Technically-unskilled users:** No software engineering or bitcoin expertise should be required. Just follow the steps.
* **Fast deployment:** Cerberus is designed to be lean and focused, so that your company can get going as quickly as possible.

### Cerberus Minimum Requirements
Acquiring all the necessary items to setup the protocol is covered in **Preparation**, but to avoid any surprises, users should ensure they will have access to the following:
* Three trusted employees
* Three [Trezor Ones](https://shop.trezor.io/product/trezor-one-white) (total cost less than USD 300)
* Three Windows/MacOS computers
* A printer
* Access to [safe deposit box](https://en.wikipedia.org/wiki/Safe_deposit_box) providers near your home or office (e.g. banks or private vaults)
* A free afternoon to follow the **Setup** section of the protocol

## Why Cerberus?

```c
"Not your keys, not your bitcoin."
- Bitcoin proverb
```

Currently, the vast majority of bitcoin storage guidance is written for personal bitcoin holdings. But a company investing in bitcoin has _very different_ security needs compared to an individual.

Due to the lack of self-storage options, companies are commonly resorting to trusted custodians. This poses serious risks, as companies' bitcoin investments are concentrated in honey pots that are highly attractive to potential attackers. A bitcoin custodian represents an easily-targeted, well-known single point of failure.

**Cerberus was produced as an easy-to-follow, quick-to-execute protocol to specifically address the unique requirements for companies self-storing bitcoin.**

Thanks to the amazing work of the bitcoin industry's open source community and entrepreneurs, Cerberus is also inexpensive to set up, making highly-secure, industry-standard storage accessible to even the smallest of companies.

## Key Concepts
To follow the protocol, users may need to first familiarise with a few key terms:

| **Wallet** | A collection of addresses with associated private keys, generated from a seed phrase. |
| **Address** | An address that can be shared with third parties who are sending your company bitcoin. A wallet consists of multiple addresses, and a new address should be used to receive each new transaction.
| **Private key** | Bitcoin transactions are controlled through private keys. Outgoing transactions must be signed with a corresponding private key. Often referred to as "key" in Cerberus for brevity. |
| **Hardware wallet** | A device used to manage private keys offline. |
| **Seed phrase** | A string of words that can be used to restore a hardware wallet. Used as a backup in case of key loss. |
| **Multisig** | A method of storing bitcoin that requires signatures from multiple private keys to make an outgoing transactions. |
| **Signatory** | An individual that manages a hardware wallet (and associated seed phrase) on behalf of the organisation. |

![Diagram of wallet structure](/assets/bitcoin_wallet_structure.png)
_A diagram showing the relationship between addresses, keys, wallets, seed phrases, and hardware wallets._

## How It Works

### Distributing Control
Cerberus uses bitcoin **multisig** to distribute control over your company's bitcoin investment across three **signatories**. Cerberus uses what's called a **2-of-3 multisig**, which means that there are three **private keys** per **address**, and at least two of those keys are required to make any outgoing transactions.

Each of the three signatories holds a **hardware wallet** which manages their set of private keys. They also store a seed phrase at a secure location that only they have access to, which acts as a backup in case anything goes wrong. Both the management and storage of the hardware wallet and seed are outlined in the protocol.

### Sending and Receiving
To receive bitcoin a transaction, any of the three signatories can provide a bitcoin address to the sender. While this is a simple process, Cerberus provides guidelines to minimise the risk of the bitcoin being sent to the wrong place.

To send a bitcoin transaction, any of the three signatories should create a transaction and sign it, before sharing the signed transaction file with one more signatory for final signature and broadcast. Cerberus provides a strict protocol for signatories to share transaction details to ensure that all outbound transactions are according to the true intent of the company.

### Issue Resolution
Finally, in the case of a hardware wallet failure, loss, or the replacement of a signatory (e.g. in the case of a staff termination), Cerberus walks you through how to resolve the issue in a secure, prompt manner.

## Structure
The protocol is split into eight sections:

| 1 | **Overview** | A brief explainer on the purpose of the Cerberus Protocol. |
| 2 | **Preparation** | All the ingredients required before you begin. |
| 3 | **Setup Ceremony** | A formal setup ceremony to ensure your company's bitcoin keys are generated in a secure environment. |
| 4 | **Receive a Transaction** | How to safely receive incoming transactions from third parties. |
| 5 | **Send a Transaction** | How to coordinate a secure outgoing transaction. |
| 6 | **Hardware Wallet Recovery** | How to restore a hardware wallet in the event of a hardware failure. |
| 7 | **Hardware Wallet Replacement** | Emergency procedures in the event of hardware wallet or seed loss, and how to replace a hardware wallet in the event of a signatory termination or death. |
| 8 | **Appendix** | All the extra background information that we ultimately decided to trim from the main protocol. Includes the kitchen sink.

| Note |
| - |
| When following the Cerberus Protocol, it's okay to read ahead, but bear in mind that the protocol is designed **so that you complete each task before moving onto the next one**. Trying to skip ahead and complete tasks to save time can lead to confusion and mistakes, potentially compromising the security of your bitcoin storage. |

## Warnings & Disclaimers

### Liability
The Cerberus protocol is used at your own risk, and the authors and contributors accept no responsibility for any losses incurred as part of the protocol's usage.

### Legal Support
Although the Cerberus is designed to minimise any potential conflicts, the protocol should still be supported by robust legal agreements between employee and the company, outlining each participant's obligations for the responsible management of funds. These agreements are beyond both the scope of this protocol and the expertise of the authors. However, should the protocol prove to be popular, we hope that some enterprising lawyers would open source some template documents!

### Accuracy of Terminology
To ensure the protocol is quickly comprehensible for newcomers to bitcoin, we have simplified some of the key terminology and definitions. Some keen-eyed bitcoiners may take issue with these compromises, but we feel that the loss of hyper-accuracy is a worthy tradeoff to ensure that secure storage is as accessible as possible.
