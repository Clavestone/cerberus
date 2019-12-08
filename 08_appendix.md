---
layout: default
title: 8. Appendix
nav_order: 8
summary: Background on the Cerberus Protocol, basic bitcoin security principles, and design notes on each of Cerberus' sections.
image: /assets/bitcoin_threats_venn.png
---

IMPORTANT: This protocol is under development and not yet ready for use.
{: .label .label-red }

Appendix
========
{: .no_toc }

The Appendix is where we store all of our more in-depth information on the Cerberus Protocol. While the main protocol sections are designed to be lean and streamlined, giving users only the most essential information to get their secure storage operational quickly, the Appendix is the opposite. It's wordy. It's where we go out of our way to provide excess detail on our design decisions.

For that reason, the Appendix is very long. To help find what you're looking for check out the contents below or try the search function in the top bar.

## Contents
{: .no_toc }

* 1: **[Cerberus Background](#1-cerberus-background)**
  * 1.1. [The Team Behind Cerberus](#11-the-team-behind-cerberus)
  * 1.2. [Project Origins](#12-project-origins)
* 2: **[Basic Bitcoin Security Principles](#2-basic-bitcoin-security-principles)**
  * 2.1. [There is No Perfect Security](#2-basic-bitcoin-security-principles)
  * 2.2. [Technology & Processes](#22-technology--processes)
  * 2.3. [Security Versus Convenience](#23-security-versus-convenience)
  * 2.4. [Corporate Versus Personal](#24-corporate-versus-personal)
  * 2.5. [Threats to Corporate Bitcoin Storage](#25-threats-to-corporate-bitcoin-storage)
  * 2.6. [Self-Storage Versus Custodial](#26-self-storage-versus-custodial)
* 3: **[The Cerberus Approach](#3-the-cerberus-approach)**
  * 3.1. [Required to Spend](#31-required-to-spend)
  * 3.2. [The Cerberus Threat Model](#32-the-cerberus-threat-model)
* 4: **[FAQ](#4-faq)**
  * 4.1. [Why Bitcoin Only?](#41-why-bitcoin-only)
  * 4.2. [Why Electrum?](#42-why-electrum)
  * 4.3. [Why Trezor?](#43-why-trezor)
  * 4.4. [Why No Passphrases?](#44-why-no-passphrases)
* 5: **[Protocol Design & Risks](#5-protocol-design--risks)**
  * 5.2. [Preparation Notes](#52-preparation-notes)
  * 5.3. Ceremony Notes _(COMING SOON)_

## 1. Cerberus Background

### 1.1. The Team Behind Cerberus

- **[Robbert Gorris](https://www.linkedin.com/in/robbertgorris/):** Delivers wealth management and corporate structuring services in Asia, with extensive experience in digital asset and DLT projects.
- **[Guillaume Verbal](https://www.linkedin.com/in/guillaumeverbal/):** Founder of Coinwallet, China’s leading bitcoin hardware wallet reseller, and Bitcoin1212. Former lead developer of the ARK wallet.
- **[Neil Woodfine](https://www.linkedin.com/in/nwoodfine/):** Working in the bitcoin industry since 2014, with experience at some of the leading bitcoin startups in exchange, payments, and infrastructure.

We couldn't have completed Cerberus alone, and have received lots of valuable input from various people in the industry. For special thanks, see our **[Contributor section](https://cerberus.clavestone.io/10_contributions.html)**.

### 1.2. Project Origins

#### The Setup
{: .no_toc }
Cerberus emerged from a commercial project to build a Bitcoin storage solution for institutions. As firm believers in the importance of bitcoin investors holding their own keys, our team wanted to provide an easy way for businesses to set up multisig storage where they held control of their bitcoin. 

We recognised that most companies today are not yet familiar with cryptography or bitcoin, and so are potentially not equipped with the necessary expertise to manage their security correctly. Also, companies face unique challenges, such as changes in staff and the threat of inside jobs, which require a unique approach compared to personal storage.

#### The Response
{: .no_toc }
To solve these problems we built a prototype of a "shared storage" solution inspired by a couple of sources:
1) Daniel Krawisz's article on [Bitcoin's Rugged Individualism](https://nakamotoinstitute.org/mempool/bitcoins-rugged-individualism/);
2) Andreas Antonopolous's [presentation at the Canadian Senate hearing](https://www.youtube.com/watch?v=xUNGFZDO8mM): _"...there are also models that are a hybrid, where a bank may have a signatory role, but is not able to change the direction of the funds. They would simply approve transactions._

In our shared storage model, bitcoin multisig keys are spread across two organisations—the owning organisation and a professional "authenticator". To release a transaction, multiple keys from both organisations are required to sign. Thus the owner can rest easy knowing the authenticator can never spend the funds on its own, while they defend against potential compromises at the owning organisation. 

#### The Complication
{: .no_toc }
However, during our trials with interested parties, we realised we were trying to achieve too much too soon, and that the world is maybe not quite ready for such a complex storage product. We decided to get back to basics.

#### The Resolution
{: .no_toc }
So we hit upon the idea of simplifying our system as much as possible, removing the second "authoriser" organisation, moving to the familiar 2-of-3 multisig configuration, and releasing an open source guide in the vein of the [Glacier Protocol](https://glacierprotocol.org/).

We still believe in the strength of a multisig shared storage model. However, a 2-of-3 multisig enforced with strict, well-defined setup and payment processes is already significantly more secure than the self-storage deployed by most bitcoin-holding companies today, and infinitely better than custodial solutions.

***

## 2. Basic Bitcoin Security Principles
This section covers general principles behind bitcoin security as we see them, and is not specific to the Cerberus Protocol. These principles are what inform our approach to building the procedures around the Cerberus Protocol. 

### 2.1. There is No Perfect Security
There is no bitcoin storage solution that can offer perfect, unbreakable security. For a determined enough attacker under the right circumstances, any storage has vulnerabilites that can be breached. 

Some solutions are more vulnerable than others, but all approaches to bitcoin storage involve a variety of tradeoffs. Improving security against one threat can sometimes decrease security against another. A custodian does not solve this problem, and in many ways makes the problem worse, as we will discuss below. 

As a basic example of a tradeoff: a hardware wallet is physically more secure than a typical internet-connected laptop, but a hardware wallet exposes users to increased supply chain risk (also discussed below).

The goal of building a secure bitcoin storage solution is to mitigate or outright eliminate the _largest risks_, and to ensure that there are checks and balances in place to detect and prevent potential compromises before they occur.

### 2.2. Technology & Processes
Any secure bitcoin storage is achieved through a combination of both technology _and_ processes. As a simple example, a user should **always** remember to cross-check the send address on a hardware wallet display before confirming a transaction. An impenetrable, unhackable hardware wallet is still vulnerable if the person using it is careless. 

Sometimes technology can help enforce processes—e.g. by prompting users to make certain checks or preventing users from initiating various dangerous commands—but ultimately any good bitcoin storage will involve strict processes that are managed outside of the hardware and software.

### 2.3. Security Versus Convenience
One of the key tradeoffs faced when building a bitcoin storage solution is between security and convenience.

When selecting a bitcoin storage solution, users are forced to make a series of subjective decisions on whether to retain a certain level of usability at the expense of security. Sometimes lower convenience can even be *part of* what makes a solution secure.

As a crude example, a user could set up a 14-of-15 multisig with two of the keys sent to a secret location on the moon. This would be very secure—no one would be spending the coins in a hurry—but this storage would be practically useless for most use cases.

Herein lies a serious problem: the more secure a storage solution is, the less convenient it will be, the less people will use it, the more funds are put at risk. Therefore the Cerberus protocol favours practical security over "absolute" security.

### 2.4. Corporate Versus Personal
Bitcoin storage for companies is fundamentally different in nature to bitcoin storage for individuals. With personal bitcoin self-storage, the owner is the same person that is in control of the bitcoin. But with corporate bitcoin storage ownership and control are split. The owning organisation _must_ entrust control of its bitcoin to one or more its agents (e.g. shareholders, board members, employees).

Some unique issues presented by the ownership-control split:

* **Motives:** The organisation's agents have independent motives, which could be out of alignment—or outright conflict—with the wider organisation's goals.
* **Motivation:** The agents may also be less motivated to properly manage the organisation's bitcoin keys in a secure manner.
* **Control transfers:** The organisation, through its agents, must also have the power to transfer control to new agents in the event of one agent's termination or death.

Multisig storage helps mitigate these issues by giving no single agent direct control over the bitcoin. With multisig, multiple agents must coordinate together to spend the organisation's bitcoin. They can verify each others' actions, better ensuring that any transaction is in line with the organisation's goals.

It should also be noted that for companies, the **[security versus convenience](#22-security-versus-convenience)** issue is worse, because people at work are busy, and unlike bitcoin hobbyists, they don't have time or patience to deal with anything heavily technical. 

Therefore it is especially important when it comes to corporate storage to eschew "absolute" security in favour of practical security.

### 2.5. Threats to Corporate Bitcoin Storage
Corporate bitcoin storage faces a variety of threats that could result in partial or total loss of the bitcoin. The first set of threats are external, and are almost identical in nature to those threats faced by personal bitcoin storage. The second set of threats are internal, a subset of which are unique to corporate bitcoin storage.

We have tried to categorise the threats here, but note that it is not exhaustive and many of the categories have some overlap:

#### 2.5.1. External Threats
{: .no_toc }
External threats are posed by individuals or groups external to the owning organisation.

| Type | Description | Examples |
| - | - | - |
| Hacks | Remote digital exploits, including installing malware on users' devices and man-in-the-middle (MITM) attacks. Often combined with social engineering. | [Mt. Gox hack](https://medium.com/@jimmysong/mt-gox-hack-technical-explanation-37ea5549f715); [Bitfinex hack](https://www.coindesk.com/bitfinex-bitcoin-hack-know-dont-know); [Binance hack](https://www.binance.com/en/support/articles/360028031711); [Evrial malware for bitcoin addresses in clipboard](https://www.bleepingcomputer.com/news/security/evrial-trojan-switches-bitcoin-addresses-copied-to-windows-clipboard/). |
| Social engineering | Using personal information to trick bitcoin key holders into inadvertently providing access to their keys. Includes phishing. | [Bitstamp hack](https://www.coindesk.com/unconfirmed-report-5-million-bitstamp-bitcoin-exchange); [Nicehash hack](https://www.theguardian.com/technology/2017/dec/07/bitcoin-64m-cryptocurrency-stolen-hack-attack-marketplace-nicehash-passwords); [Custodial wallet hack](https://medium.com/@CodyBrown/how-to-lose-8k-worth-of-bitcoin-in-15-minutes-with-verizon-and-coinbase-com-ba75fb8d0bac); [Foiled Coinbase hack attempt](https://www.coindesk.com/coinbase-says-it-foiled-a-sophisticated-hacking-attack). |
| Physical theft | Stealing keys or seed phrases. Includes non-violent thefts such as break-ins and "evil maid" attacks, and violent thefts such as mugging and hold-ups. | [Armed home invasion of Localbitcoins trader](https://localbitcoins.com/forums/#!/general-discussion:armed-break-inhome-invasio); [Masked raiders hold up Bitcoin Exchange in front of dozens of witnesses](https://archive.fo/fAoh0); [Man raided in office](https://archive.fo/HHicH); [comprehensive list of physical attacks on bitcoin key holders](https://github.com/jlopp/physical-bitcoin-attacks/blob/master/README.md). |
| Kidnapping | Similar to some forms of physical theft, kidnapping involves the confinement of a key holder or someone related to the keyholder in order to coerce bitcoin keys, a PIN, or a transaction from the key holder. | [Cryptocurrency executive kidnapped at car wash](https://archive.fo/VDAjq); [Wife of crypto exchange owner kidnapped and ransomed](https://translate.googleusercontent.com/translate_c?depth=1&hl=en&prev=search&rurl=translate.google.com&sl=pt-BR&sp=nmt4&u=https://www1.folha.uol.com.br/cotidiano/2017/05/1880569-bandidos-pedem-dinheiro-digital-para-libertar-refem-de-sequestro.shtml&xid=17259,15700002,15700019,15700124,15700149,15700168,15700186,15700190,15700201,15700208&usg=ALkJrhh0Ok2Seoc85twz3X488yGHyzXjkw); [Bitcoin trader tortured with drill](https://archive.fo/UONTD); [comprehensive list of physical attacks on bitcoin key holders](https://github.com/jlopp/physical-bitcoin-attacks/blob/master/README.md). |
| Blackmail | Threatening to reveal compromising or damaging information about a key holder to coerce bitcoin keys, a PIN, or a transaction from them. | [Foiled Binance blackmail attempt](https://www.engadget.com/2019/08/07/binance-cryptocurrency-exchange-blackmailed-over-customer-data/); [Blackmail spam scam](https://www.theguardian.com/technology/askjack/2019/jan/17/phishing-email-blackmail-sextortion-webcam). |
| Supply chain attack | Software or hardware compromises introduced into bitcoin hardware (e.g. hardware wallets and laptops) during manufacture, or at any stage of the subsequent logistics process. | [Demo of supply chain attack on Ledger](https://thenextweb.com/hardfork/2018/03/20/ledger-nano-s-hack-cryptocurrency/); [Fake Trezors on the market](https://blog.trezor.io/psa-non-genuine-trezor-devices-979b64e359a7). |
| State intervention | Government agencies taking arbitrary actions to freeze, seize, or confiscate bitcoin holdings. Bitcoin's competition with central banking means it is difficult to predict how various governments will react to its continued success. | [Executive_Order_6102 (the US gold ban)](https://en.wikipedia.org/wiki/Executive_Order_6102); [Aryanization](https://en.wikipedia.org/wiki/Aryanization); [Cyprus bank deposit levy](https://en.wikipedia.org/wiki/2012%E2%80%9313_Cypriot_financial_crisis); [Civil Asset Forfeiture](https://en.wikipedia.org/wiki/Civil_forfeiture_in_the_United_States). |

An important distinction to note on external threats for corporate bitcoin holders is that, unlike with personal holders, threats are posed to _signatories of the holder_ rather than the holder itself (which is just a legal, virtual entity). This results in two unique problems:
1. **Signatories must take on personal liability and personal risk on behalf of the organisation:** Successful hacks or social engineering may lead to accusations of negligence. Physical theft, kidnapping, blackmail, and state interventions may pose physical risks to a signatory even though they do not directly own the funds. 
2. **Agents are less incentivised to protect the funds than their own personal holdings:** At best, a signatory will have indirect, partial ownership of the bitcoin held by the organisation (e.g. a shareholder). There are many factors at play (e.g. relative ownership values), but in many cases it is likely that a signatory would go to less lengths to protect their organisation's bitcoin keys than they would to protect their own personal bitcoin keys—regardless of the individual's intergrity or how committed they are to their organisation.

On first glance, the immediate conclusion might be that custodians would solve these issues. They do not. In many ways they make the problem worse by expanding the number of agents to the organisation that are under threat. See section **[2.5. Self-Storage Versus Custodial](#25-self-storage-versus-custodial)** for details.

#### 2.5.2. Internal Threats
{: .no_toc }
Internal threats are posed by individuals working for the owning organisation.

| Type | Description | Examples |
| - | - | - |
| "Fat fingers" | Sending to a wrong address; sending the wrong amount; receiving to the wrong address; using the wrong transaction fee. | [Accidental 30BTC transaction fee](https://www.reddit.com/r/Bitcoin/comments/1eh57i/messed_up_transaction_feeplease_help/); [Accidental 100 BTC transaction fees](https://bitcointalk.org/index.php?topic=296217.0;all); [Accidental 80BTC transaction fee](https://blog.btc.com/accidentally-pay-an-80btc-transaction-fee-please-contact-us-for-a-refund-b9f8bb4ff65a); [Sent BTC to BCH address](https://bitcointalk.org/index.php?topic=2333267.0); [Sent bitcoin to the wrong address](https://bitcoin.stackexchange.com/questions/45729/incorrect-bitcoin-address-funded?noredirect=1&lq=1); [Dumbest mistakes users have made with bitcoin](https://www.reddit.com/r/Bitcoin/comments/1gglsq/dumbest_mistake_youve_made_with_bitcoin/). 
| Carelessness | Key loss; seed phrase loss; seed phrase recording error; revealing keys publicly through careless key management. | [Man who accidentally threw away hard drive carrying 7,500 BTC](https://www.cnbc.com/2017/12/20/man-lost-127-million-worth-of-bitcoins-and-city-wont-let-him-look.html); [Lost bitcoin wallet and incomplete seed phrase](https://bitcoin.stackexchange.com/questions/78987/lost-my-bitcoin-wallet-and-have-only-11-out-of-12-mnemonic-seed-phrase-words-ho). | 
| Inside jobs | Shareholders, employees, or contractors stealing bitcoin under custody (usually indistinguishable from external attack). | [(Suspected inside job) Cryptsy hack](https://www.coindesk.com/8-2-million-court-orders-default-judgment-cryptsy-ceo); [(Suspected inside job) Sheep Marketplace hack](https://www.theguardian.com/technology/2013/dec/03/online-drugs-marketplace-shut-down-bitcoin-hack-sheep). |
| Terminations | Internal disputes; people leaving the organisation; deaths. | [QuadrigaCX exchange owner allegedly dies taking exchange holdings with him](https://bitcoinmagazine.com/articles/quadrigacx-and-the-million-dollar-questions-what-we-do-and-dont-know); [Johann Gevers withholding Tezos crowdfund private key during dispute](https://www.wired.com/story/tezos-blockchain-love-story-horror-story/).

Internal threats faced by personal and corporate bitcoin storage alike:
- "Fat finger" errors
- Careless key management 

Internal threats that are unique to corporate storage, and require special processes to minimise their probability of occuring:
- Inside jobs
- Terminations

Of all the internal threats, **inside jobs** are particularly pernicious because they can be impossible to distinguish from a successful external attack. An employee secretly sending his organisation's bitcoin holdings to an address he controls can claim that he was hacked and it is difficult to impossible for any outside observers to tell otherwise (unless he turns up to work in a Lamborgini the next day!).

Inside jobs in corporate bitcoin storage come with signficant _plausible deniability_.

#### 2.5.3. People Risk
{: .no_toc }
By far the biggest threat to bitcoin storage security (or information security in general) is _people_. In contrast to the mechanical nature of software and hardware, people are complex, unpredictable, and have many vulnerabilities. The "wetware" is where most things go wrong.

This can be seen in the above threats, of which only hacks, supply chain attacks, and state interventions fall outside of the "human risk" category. Broadly, we're talking about:
- people making mistakes
- people being tricked
- people being attacked
- people acting maliciously

No amount of hardware or software can fully resolve these threats. Although they can sometimes make them easier to resolve, for instance, through user-friendly dedicated hardware and multisig.

Instead, properly reducing people risk requires fighting fire with fire: real world, meatspace, human processes. This means strict rituals and checklists which:
- ensure each signatory knows what they should be doing, when they should be doing it
- reduce the chances of signatories making mistakes
- ensure no one person is a single point of failure
- require confirmations from multiple signatories for any actions 
- require sufficient review for others to spot any mistakes or malicious data before they go into a broadcast transaction
- encourage signatories to regularly pay attention to their own physical security

##### Categories of Threats to Bitcoin Holdings
{: .no_toc }
![Categories of Threats to Bitcoin Holdings](/assets/bitcoin_threats_venn.png)

### 2.6. Self-Storage Versus Custodial
After a never-ending series of custodial failures, **individuals are already well aware that safe bitcoin storage means holding their own bitcoin keys**.

But as we enter a new stage in bitcoin adoption, many organisations are starting to acquire bitcoin as an investment, and they are instead choosing the easy option of storing their keys with bitcoin custodians. Over time, these organisations will be taught expensive lessons in the importance of independent key storage.

Bitcoin is liquid, borderless, and very difficult for law enforcement agencies to exert any influence over, making it an attractive asset for thieves. A bitcoin custodian compounds this problem by a establishing a centralised honey pot—a thief only needs to compromise the custodian to gain access to _all_ of their clients' funds.

While high-profile hacks have been limited to cryptocurrency exchanges and individuals now, it is likely that we are going to see some compromises of previously respectable custodians over the next decade. This including ETFs and other bitcoin investment vehicles. Bitcoin insurance is limited as-is, and will become increasingly inadequate as the value of bitcoin grows.

#### 2.6.1. Custodians Are Not Safer
{: .no_toc }
With so many threats posed to an organisation's bitcoin holdings, it may seem at first glance that it's a lot safer and easier to go with a custodian. However, using a custodian poses a new set of problems:
1. **Threats redirected:** It does not eliminate any of the internal or external threats. Instead, it simply shifts them to a third-party. 
2. **Targets multiplied:** For many of the threats, it doubles the number of parties exposed to them—both the custodian *and the owner* can be compromised.
3. **Increased Risks:** Professional custodians represent centralised targets with high concentrations of funds—optimal targets for external threats and inside jobs.

#### 2.6.2. Threats Redirected
{: .no_toc }
A custodian faces the exact same set of internal and external threats as an organisation holding their own bitcoin keys. For example, signatories at the custodian can engage in inside jobs, make mistakes, or be targeted by thieves, the same as any signatory at the owning organisation.

Due to the funds held under management by a custodian not belonging to the custodian, they have less skin in the game. Faced by certain threats such as blackmail or a state intervention, they may be less inclined to act in the owners' interests.

#### 2.6.3. Targets Multiplied
{: .no_toc }
The threats are not only shifted to the custodian's signatories. A custodian must provide permissions to one or more agents at the owning organisation to make transactions under certain conditions.

The procedures around confirming transactions can help mitigate some threats, but the owning organisation's agents are ultimately able to direct the custodian's signatories to make irreversable, difficult-to-trace transactions on their behalf.

These agents can still be targetted by hacks, social engineering, kidnapping, and blackmail. They are sometimes even better targets because it only takes one.

In summary, by using a custodian, not only can the custodian's signatories be compromised, but the owner's agents can be too, increasing the storage's attack surface.

#### 2.6.4. Increased Risks
{: .no_toc }
As can be seen from the long history of bitcoin exchange hacks, custodians are prime targets for malicious actors. Successful custodians (and who would want to select an unsuccessful custodian?) hold enormous amounts of bitcoin under management.

Compromising secure multisig bitcoin storage involved serious planning and risk, so custodians represent a better use of time for would-be attackers—they get a much higher ROI on their efforts. Furthermore, custodians are typically high-profile organisations, thus attracting more attempts at compromising their holdings.

With an increased concentration of funds also comes a greater temptation for the custodian's signatories to commit an inside job. And remember—inside jobs in bitcoin [come with plenty of plausible deniability](#2.4.2.-Internal-threats).

#### 2.6.5. Where Custodians Might Help
{: .no_toc }
Custodians can provide convenience by taking over the responsibilities software management, hardware management, and transactional procedures. Setup and transactions can be completed much faster, with a phone call for example.
**But it comes at the cost of security**, as described above.

Compared to an inexperienced team hastily deploying bitcoin storage on an online Windows laptop, without any explicit protocol, custodians may also represent a better alternative. However, with some time, patience, and a little simple guidance, any team is capable of setting up their own secure bitcoin self-storage, without having to expose themselves to the risks of a third-party custodian.

This is where Cerberus comes in. It provides simple directions for teams to set up and manage their own secure corporate bitcoin storage, with no experience required.

#### 2.6.6. Storage Portfolios
{: .no_toc }
In the cryptocurrency industry it's common to hear that "coin portfolios" are a great way to hedge risk. This is questionable at best, because cryptocurrencies are typically mostly correlated with each other (and [altcoins have problems of their own](https://nakamotoinstitute.org/mempool/the-problem-with-altcoins/)).

The real "hedged risk" portfolio strategy in bitcoin is storage portfolios. As simple as "don't put all your eggs in one basket."

Spreading bitcoin across two or more storage methods is a generally a good idea and one the authors of the protocol endorse. Cerberus would work very well as one of the options in such a portfolio.

A custodian could be justified in a storage portfolio, but it is recommended to keep a minority of holdings with the custodian, given the risks posed by fund centralisation.

#### 2.6.7. Delegation of Responsibility
{: .no_toc }
One of the biggest drivers behind companies selecting bitcoin custodians is the tendency for employees to prefer delegating responsibility. They don't want to get blamed if something goes wrong.

This is in stark contrast to individual bitcoin holders, who take more responsibility for their wealth and typically opt for self-storage options.

We only have one thing to say on this topic: you might not get fired for selecting a big-name custodian, but you could lose your organisation a lot of bitcoin.

***

## 3. The Cerberus Approach
Cerberus thoroughly considers corner cases such as obscure vectors for malware infection, key holder terminations or deaths, coordinated “Ocean’s Eleven” heists, sophisticated social engineering, state-level confiscations, and so on. Even if your organisation’s bitcoin holdings are more modest, it's worth considering using Cerberus. When bitcoin proves successful as a global money, it will appreciate 10x (or much more) in the coming years. Security will become increasingly important if your holdings appreciate and Bitcoin becomes a more attractive target for thieves. 

### 3.1. Required to Spend
Understanding what combinations of data are required to spend in bitcoin multisig storage can sometimes be a little confusing. With Cerberus, there are four key pieces of sensitive data:
- The hardware wallet device
- The hardware wallet PIN
- The seed phrase
- The master public key (_"xpub"_)

Each of these pieces of data has no value on its own, but certain combinations can be used to spend the organisation's bitcoin funds (either by an attacker or by the organisation itself in an emergency situation):

![Spending Conditions for 2-of-3](/assets/spending_conditions.png)

**SPENDING REQUIRES:**
- Any three of:
    - Seed phrase
    - Hardware wallet + PIN*

**OR:**
- Any two of:
    - Seed phrase
    - Hardware wallet + PIN*
- Plus one of:
    - xpub belonging to the remaining key

| NOTE: with a combination of physical access to device, sufficient technical proficiency, and specialised hardware, it is possible for someone to extract the keys from the hardware wallet without the PIN. |
| - |

### 3.2. The Cerberus Threat Model
To deliver a convenient solution, Cerberus is built on a set of assumptions about the technology used and the people operating it. Cerberus is designed so that understanding these assumptions is not essential for the safe operation of the multisig storage. However, these assumptions should be considered threat vectors or risks, and it's better that they are made explicit for the purposes of community review.

#### 3.2.1. Recipient Address Accuracy
{: .no_toc }
Regardless of how well you secure your stored funds from external and internal thefts, if you send a payment or receive a payment to the wrong address, your funds are still lost.

Currently there are no commonly used methods for verifying that a bitcoin address belongs to a certain entity.

As part of the **Receiving a Payment** and **Sending a Payment** sections, Cerberus guides signatories to minimise the risk of:
1. Human error
2. External parties replacing the correct address with a malicious one

But, ultimately, there is little that can be done about a compromised agent working at your counterparty. Some methods of minimising this risk are:
- Minimise the number of counterparties your business transacts with
- Minimise the number of transactions your business makes

#### 3.2.2. Security Over Privacy
{: .no_toc }
The Cerberus protocal prioritises security over privacy. 

While there are some great privacy-enhancing technologies emerging in the bitcoin industry, and privacy is tangential to security, the existing solutions available would introduce too much complexity to the protocol.

The goal of Cerberus is to achieve adoption even amongst companies with little bitcoin experience. Until privacy solutions improve in terms of their UX, or combined with multisig wallet functionality, they cannot be included in Cerberus for fear of reducing adoption. Secure multisig bitcoin holdings outside of the hands of custodians is essential for a healthy bitcoin industry.

As soon as privacy solutions are significantly improved, we will be more than happy to introduce them into Cerberus.

A non-exhaustive list of privacy compromises are outlined here:

##### Multisig visibility
{: .no_toc }
Cerberus uses a multisig wallet to provide superior security compared to single key storage solutions. However, few wallets today use multisig, and when a bitcoin transaction is made from a multisig wallet, the parameters of the wallet are revealed on the blockchain:
1. The number of signatories in the wallet
2. The signature format specific to the wallet used
3. The public key of each signing signatory 
4. The bitcoin address the funds were sent from
5. The bitcoin address the funds were sent to
6. The amount sent

This means that multisig transactions "stand out" more on the blockchain. If an organisation uses unusual multisig parameters (e.g. a 4-of-9), or a custom wallet, and a third party out there somehow knows that this is the case, then they can potentially identify the organisation's transactions in real time with a high degree of accuracy.

Thankfully, Cerberus uses one of the most-used multisig formats (2-of-3) generated by the most-used wallet software for multisig (Electrum). This means any transaction sent from a Cerberus wallet will look identical to transactions from many other wallets, and be more difficult to trace back to the organisation making it based only on the transaction format.

Still, multisig transactions are more unusual than single signature transactions, and provide more potential identifiers for third parties monitoring financial activity on the bitcoin network.

#### 3.2.3. Assume Compromise After Physical Access
{: .no_toc }
If anyone other than the signatory gains physical access to a hardware wallet—e.g. in a theft or after losing one for period of time before getting it back—the key should be considered compromised. 

Online, there are numerous accounts of white hat hackers accessing the keys contained within hardware wallets within only a few minutes of access to the device. These vulnerabilities typically get patched very quick, require  significant technical knowledge to achieve and dedicated hardware. However, with large values of bitcoin at stake, better to be safe than sorry.

Multisig significantly mitigates this threat, as any attacker would require prolonged access to at least two devices (and a third key or xpub—see **[Required to Spend](#31-required-to-spend)**) to be able to spend any coins.

After discovering that a third party gained or may have gained physical access to one of the hardware wallets, signatories should immediately make efforts to move the stored coins to a new multisig wallet according to the key replacement section of the protocol.

#### 3.2.4. The MC is Trusted During the Ceremony
{: .no_toc }
To ensure reliable execution of the setup section of the protocol, we came to the conclusion that it was necessary for one person to lead the setup ceremony. Each signatory needs to know what to do and when, and it would be difficult to coordinate this with each signatory reading from the protocol independently.

Also, people tend to be extremely busy at work, and we decided that expecting all three signatories to closely familiarise themselves with the protocal may be a bridge to far.

The MC has an important role during the setup of the Cerberus protocol. The MC purchases the required hardware, arranges the venue, and directs the signatories during the setup ceremony.

Therefore, the MC has an opportunity to introduce compromised hardware, install recording devices at the venue, or alter the protocol as he provides instructions.

As such the MC should be assumed to be trustworthy *during the setup ceremony only*. Following a successful setup, if the MC later turns malicious or is compromised, then the multisig nature of the bitcoin storage will ensure the organisation's funds are safe as long as the other two signatories are honest actors.

While we suggest that the MC is assumed to be trusted during the ceremony, Cerberus still includes the following instructions to increase the risk of other signatories detecting any anomalies:
1) Each signatory prints out their own version of the protocol, and reads through the document themselves during the execution of the setup ceremony.
2) Fully packaged hardware wallets are checked by all three signatories for authenticity before opening at the ceremony.

Another option to improve security would be to introduce an independent observer, e.g. a lawyer or notary, to observe the setup ceremony. The independent observer should have also familiarised themselves with the protocol to verify that procedures are being followed correctly. The reason why we have not made this a part of the protocal is that it introduces an extra layer of complexity that provides a marginal increase in security.

#### 3.2.5. Supply Chain is Trusted
{: .no_toc }
_Coming soon._

***

## 4. FAQ

### 4.1. Why Bitcoin Only?
There are already plenty of resources that [explain the issue with altcoins](https://nakamotoinstitute.org/crash-course/) on both a technological and economic level.

Bitcoin is by far the most secure and mature technology in the cryptocurrency space (or to put it another way: altcoins are insecure). To provide guidance on securing multiple different coins using different technologies would dilute the protocol, require compromises to accomodate multiple approaches at the same time, and ultimately still leave holders open to the insecurities that exist at altcoins' protocol layers.

Providing support for altcoins is not something that interests the authors and we would robustly advise against businesses investing in them.

### 4.2 Why Electrum?
Electrum is quite simply the best solution for building custom multisig self-storage today. It is fully open source, and after being around for years has been well-audited by the developer community. For now, nothing else comes close in terms of reliability and flexibility.

The only other open source wallet we are aware of that provides custom multisig features is Copay, but this software has been languishing the past few years and is now an inferior solution.

The main downside of using Electrum is the privacy implications of connecting to random Electrum servers. For discussion on this, see the **[Security Over Privacy](#322-security-over-privacy)** section.

Some people might wonder why we don't use Electrum's in-built "Cosigner Pool" feature in Cerberus—it appears to be an undersupported feature and extremely buggy, and we eventually gave up trying to force it to work!   

### 4.3. Why Trezor?
It is important to point out that the Cerberus Protocol is not tied to any one hard wallet or manufacturer. Based on developments in the industry, and feedback from reviewers, we may choose to change the hardware wallet recommendation at a later date.

Technically, Cerberus' focus is on the _procedures_ around organisational multisig management, therefore most hardware wallets should already be suitable to replace our current selection. However we'd recommend only the most expert of expert bitcoin users attempt this. For everyone else, we have made the selection of the Trezor One very carefully, taking into account security, usability, and historic track record. 

| Hardware wallet | Pros | Cons | 
| - | - | - |
| Trezor One | Longest track record, exploits are well known; fully open source software _and_ hardware; very user-friendly; low-cost. | Known to be vulnerable to physical exploits; requires USB connection. |
| Ledger Nano S | Long track record, most commonly-used wallet, exploits are well known; user-friendly post-setup; low-cost. | Support for multiple tokens diffuses security focus; requires USB connection; our own tests found setup to be unfriendly; encountered multiple small bugs when pairing with Electrum; doesn't support verification of multisig receive & change addresses on-device (offloading verification to the user and potentially-compromised laptops). |
| Coldcard | Bitcoin-only support allows team to focus more resources on security; fully open source software _and_ hardware; [PSBT](https://github.com/bitcoin/bips/blob/master/bip-0174.mediawiki#Abstract) support; on-device PIN entry; full air-gap support; seed self-generation support (e.g. with dice) reduces supply chain risk; low-cost. | Newer solution with fewer users so potential exploits less well known; looks more daunting to non-technical users; sold in batches meaning not always available. |

For now we've settled on the Trezor One mainly thanks to its long track record of being a secure storage solution, and its simple and friendly user interface.

Growing list of hardware wallet alternatives with multisig support:
- [BitBox](https://shiftcrypto.ch/)
- [CryptoAdvance](https://cryptoadvance.io/)

For anyone interested in diving deeper into comparing hardware wallets, we'd recommend [this comprehensive comparison resource from Michael Flaxman](https://bitcoin-hardware-wallet.github.io/) (Keepkey, Ledger Nano S, Trezor Model T, and ColdCard only for now).

| NOTE: The protocol contributors do not receive any commissions or referrals from our hardware wallet recommendations, instead preferring Cerberus to remain independent.
| - |

### 4.4. Why No Passphrases?
_Coming soon._

***

## 5. Protocol Design & Risks
This section breaks down the Cerberus protocol step-by-step, providing:
1. Background on the design decision behind individual instructions and recommendations;
2. Details of potential threats to watch out for (remember, no security is perfect).

The notes are numbered according to the section headers in the main protocol, prepended with a 5. For example, if you're specifically looking for an explanation for [chapter 2 ("Preparation"), section 3.1], you should head to 5.2.3.1.

### 5.2. Preparation Notes

#### 5.2.1. Assembling the team
{: .no_toc }

##### 5.2.1.1. Select the signatories
{: .no_toc }
The Cerberus protocal uses a 2-of-3 multisignature Bitcoin wallet. This means that any two of three keys need to sign a transaction before it can be executed. Each signatory should only hold one key. If any signatory holds more than one key, the multisignature setup has little to no value, because that signatory has the power to make transactions without the confirmation from anybody else.

Likewise, each key should only be held by one individual. Giving multiple signatories access to one key would:
1. Increase the attack surface for compromising the key
2. Provide each of the key's holders with plausible deniability in the event of a rogue transaction—it would be impossible to verify which of the holders signed the transaction.

When selecting the signatories, the more skin in the game each signatory holds with the organisation, the better. The signatories need to deeply care about the security of the bitcoin held by the organisation so that they strictly stick to the protocol.

##### 5.2.1.2. Assign a number to each signatory
{: .no_toc }
Originally we considered having the protocol executed on a more ad-hoc basis, with any signatory allowed to initiate a transaction, and any other signatory allowed to pick up the transaction, confirm, sign and broadcast.

However, we realised that unless each signatory knows exactly what they should be doing at all times, then the ambiguity will lead to a) time consuming discussion and coordination with fellow signatories, and b) more room for errors to be made.

By having clearly defined roles within the protocol, each signatory will achieve clarity on their responsibilities and become very familiar with the associated procedures required by their role.

The protocol also mimics an organisational structure where there is a CFO, controller, administrators, etc.  We expect this person would fill the Signatory 1 role. 

Of course, technically any signatory can initiate and confirm a transaction, but doing so out of order should be considered a violation of the protocol. Violations of protocol put your bitcoin funds at risk and should be reserved for emergencies.

One risk of having a explicit signatory order is that it is potentially more easily socially engineered. It is therefore of the utmost importance that Signatories 2 and 3 diligently perform their transaction verification duties and do not automatically sign transactions issued by Signatory 1. 

##### 5.2.1.3. Designate a “Master of Ceremony” (MC)
{: .no_toc }

See section 3.2.5. **["The MC is Trusted During the Ceremony"](#325-the-mc-is-trusted-during-the-ceremony)**.

***

#### 5.2.2. Print Out The Cerberus Protocol
{: .no_toc }

Although following the protocol on a screen may seem more convenient, having a physical copy allows tasks to be ticked off with a pen to create a persistent record of progress, making it less likely for signatories to lose their place or make mistakes.

Note that it is assumed that the Preparation and Setup Ceremony sections on the Cerberus website have not been compromised at time of printing. Potential risks include the insertion of instructions that make key creation insecure, performed by:
1) The Cerberus contributors themselves
2) An external party that has compromised the GitHub login credentials of a contributor 
3) GitHub employees with access to user repositories
4) An external party that has maliciously redirected GitHub's server or Clavestone's domain traffic
5) An external party that has compromised the signatory's local network, device, or printer

We considered requiring the users of Cerberus to download the full protocol and cryptographically verify it's authenticity, but decided that this would:
1) Increase the complexity of the protocol to a level that would reduce real-world usage.
2) Only offer minimal, perhaps even misleading, security benefits: if the protocol is compromised by contributors, GitHub, or external parties, it would be trivial for them to also direct users to use a compromised public key for the verification of the protocol, or remove the verification step entirely.

Instead, we have taken the following measures to increase the security of the protocol content:
1) Only two of the Cerberus contributors have commit access to the Cerberus GitHub repo, and only one contributor typically has the responsibility for committing updates (nwoodfine).
2) Each contributor's GitHub account is protected by a strong, unique password and 2FA.
3) Only two of the Cerberus contributors have admin access to the Cerberus domain hosting account.
4) Each admin account is protected by a strong, unique password and 2FA.
5) The Cerberus team all have email alerts set for any changes to the GitHub repo, which allows us to act and sound alarm bells if we see any changes that do not coincide with our own GitHub commits.
6) The Cerberus team all use a third-party service to monitor for changes to the content on the Cerberus website (cerberus.clavestone.io), which allows us to act and sound alarm bells if we see any changes that do not coincide with our own GitHub commits.
7) Cerberus is public and open source, meaning that any malicious changes will likely be spotted by other bitcoiners who will post public alerts on public forums like Twitter and Reddit.
8) Each signatory prints their own copy of the protocol, and follows it in parallel with the MC's instructions during the Setup Ceremony. This way, any man in the middle attacks would need to target all three signatories, otherwise inconsistencies will be spotted during the execution of the protocol at which point the process can be terminated.

##### 5.2.2.1 Print out the Preparation section
{: .no_toc }

N/A

##### 5.2.2.2. Print out the Setup Ceremony Section
{: .no_toc }

N/A

##### 5.2.2.3. Store the printed documents in a secure location
{: .no_toc }

An attacker could switch the printed documents for compromised documents before the execution of the Setup Ceremony, hence the need to store them in a secure location.

Again, by having three independent sets of documents, held in different locations under lock and key, an attacker would face the challenge of having to compromise all three without any signatory discovering, otherwise inconsistencies will be spotted during the execution of the protocol at which point the process can be terminated.

The biggest threat here is inside jobs—either by fellow signatories, or colleagues—hence the recommendation to store at home rather than the office, ensuring all the documents are held in separate, harder-to-get-to locations.

##### 5.2.2.4. Use the printed version from now on
{: .no_toc }

N/A

***

#### 5.2.3. Preparing Secure Physical Storage
{: .no_toc }
Bitcoin storage needs backups, in the form of seed phrases, in case of hardware wallet loss/damage/malfunction.

While "seedless" solutions from companies like [Casa](casa.keys) are certainly attractive, reducing the number of pieces of sensitive data that needs to be protected, they rely on larger sets of multisig keys (e.g. Casa uses 3-of-5) which provides sufficient redundancy in case of multiple key losses.

Cerberus is based on 2-of-3, which leaves little wiggle room. And personally, we'd personally sleep sounder at night knowing that each and every key can be recovered if necessary.

Each signatory in the Cerberus multisig already carries the burden of storing and protecting a hardware wallet, and usually would not have a second suitable location to store another piece of data. Therefore the decision was taken to outsource this to professional secure storage parties.

##### 5.2.3.1. Identify a safe deposit box provider
{: .no_toc }

Safe deposit box providers have long histories of protecting people's valuables but are not infallible. In times of political and economic turbulence, there are examples of these kinds of institutions being compelled to confiscate deposit box owners' property on behalf of the government, or just simply mismanaging the contents themselves. Therefore we have recommended certain criteria to mitigate the risks these third parties pose to the bitcoin storage:

###### Each signatory should use a different provider
{: .no_toc }
By keeping each seed phrase with a different provider, all three of the providers need to collude to gain access to the bitcoin. To mitigate against this risk even further:
1) Signatories sign up for each deposit box under personal accounts, to make it more difficult for anyone to connect the accounts at different providers together.
2) Each seed phrase is protected by a further level of security in the form of a passphrase, which ensures that anyone that does gain access to the contents of all three of the deposit boxes cannot immediately spend the funds.
  
###### A private vault provider
{: .no_toc }
A key advantage of the private vault provider over a bank is that it is more difficult for governments to:
- Seize the contents—private vaults tend to have stronger protections than the hyper-compliant banking sector.
- Block access to safe deposit boxes—e.g. by declaring a bank holiday.
One may think, "when does this ever happen though?" But it does. For example, during the financial crisis in Cyprus in 2012, the contents of safe deposit boxes in Cypriot banks were seized. This was possible thanks to bank safe deposit boxes being heavily regulated, in addition to being subject to the complex requirements, restrictions, and guidelines that banks normally operate under. 

That said, we recognise that many companies using the Cerberus protocol may not be located in a region with many safe deposit box options. 

It should be noted that while an attacker who gains access to all three of the seed phrases can reconstruct the wallet and gain access to the bitcoin, this does does not mean that the funds are necessarily gone. Signatories should still have access to the private keys in the form of hardware wallets. If at any time it becomes apparent that deposit boxes are being compromised, the signatories can take emergency action to move the funds to a new wallet constructed from new private keys which the seed phrases at the deposit boxex do not have access to.

###### Accessible 24/7 including public and bank holidays
{: .no_toc }
Private vaults often provide their client 24/7 access to their safe deposit box, unlike banks which will normally only provide limited access during banking hours, with advance notice often being a requirement.

In case of emergency, ideally you want to know you will always have access to the seed phrase.

##### 5.2.3.2. Book the safe deposit box
{: .no_toc }
Safe deposit boxes should be booked personally under each signatory's own name for two key reasons:
1. To ensure only one person has access to the safe deposit box. If the boxes were registered under the organisation, then numerous other members of staff—including fellow signatories—could potentially collect all three seed phrase backups without requiring the help of each individual signatory.
2. To obfuscate the relationship between the three deposit boxes. Registering them under separate names will make it more difficult for safe deposit box providers to "connect the dots" and collaborate to seize the funds (for whatever reason).

##### 5.2.3.3. Prepare home storage for hardware wallet**
{: .no_toc }

Hardware wallets must be:
1. Stored separately from each other: otherwise an attacker that compromises a single location can gain access to the bitcoin funds;
2. Stored separately from the seed phrases: the entire point of the backup is to be secured separately in case anything happens to the hardware wallet, ensuring signatories always have access to their keys.

This means they cannot be stored at the owning organisation's office, nor can they be stored in the safe deposit boxes.

The hardware wallets also need to be sufficiently convenient to access that the signatories can make transactions when required. For example, requiring a second set of safe deposit boxes would significantly increase the complexity of setting up protocol (who has six different safe deposit box providers in their local area?) and it would become very cumbersome to initiate any single transaction.

Therefore we recommend that signatories hold the hardware wallets at home in secure storage, i.e. under lock and key. Not everyone has a home safe, and cheap home safes are little better than a locked cupboard in terms of keeping determined thieves out. Requiring that all three signatories purchase a professional home safe significantly increases the cost of executing the protocol, and would reduce usage. Furthermore, there is also some small security benefits to making the location of the hardware wallet less obvious.

The multisig configuration of Cerberus bitcoin storage ensures that the bitcoin funds are still very safe when stored at home. Any thieves would have to compromise at least two, and probably _all three_ of the storage locations, plus PINs, plus passphrases (see the **[Required to Spend](#31-required-to-spend)** section) to gain access to the organisation's bitcoin funds.

Nevertheless, the signatories should fully understand and accept the responsibility they are undertaking by placing such valuable data in their own homes.

***

#### 5.2.4. Preparing the Laptops and Software
{: .no_toc }
  
##### 5.2.4.1. Prepare laptop computers
{: .no_toc }
We considered providing support for Linux, but ultimately decided that the vast, vast majority of business users will be working on Windows and macOS devices. Each additional operating system expands the guide considerably, so we opted against the Linux addition. If the protocol proves popular and there is demand for Linux support, then either we or the community can submit some updates.

##### 5.2.4.2. Download Electrum
{: .no_toc }
See the **[Why Electrum?](#42-why-electrum)** section.

##### 5.2.4.3. Install Electrum**
{: .no_toc }
N/A

##### 5.2.4.4. Verify the Electrum installation**
{: .no_toc }
This is easily the most technical part of the protocol, and may be daunting to many non-technical business users. To avoid this we looked at various different approaches that would avoid this requirement, but ultimately they all involved too much risk.

There is huge financial incentive for malicious hackers to compromise Electrum downloads, delivering compromised wallet software to users around the world. There are many possible ways for hackers to achieve this, and they are typically very creative, motivated people.

There's no way around it: **users absolutely must verify the authenticity of their wallet software if they are going to use it to hold significant volumes of Bitcoin.**

We've tried to make our verification guides as clear as possible, without taking any knowledge for granted, and hope this minor inconvenience won't put off too many users from proceeding with the protocol. Learning to verify software is an important skill in itself, and will become increasingly important as the Bitcoin industry grows.

If anyone is struggling with this section, we would recommend getting together with the other signatories, so that you can go through the process while helping each other.
    
##### 5.2.4.5. Prepare the hardware
{: .no_toc }
N/A

***

#### 5.2.5. Acquiring the Equipment
{: .no_toc }

##### 5.2.5.1. Hardware wallet purchases
{: .no_toc }
See the **[Why Trezor?](#43-why-trezor)** section.

##### 5.2.5.2. Amazon purchases
{: .no_toc }
- **Tamper-evident deposit bags:** used to store the seed phrases and seed generation. Signatories need to know if the seed phrase has been tampered with when they inspect the package at the safe deposit box.
- **Fine-point Sharpies:** Technically any pen will do, but who has some pens lying about in the office these days? Also the soft nibs of the Sharpies insure no impressions will be made on the surface below the seed phrase cards.
- **Privacy screens:** Only one is required to prevent other signatories observing the recording of the seed phrase during the setup ceremony, but these are always sold in multi-packs.

These items should remain sealed in their original packaging until the day of the ceremony, when they should be opened in front of all the signatories. This way the signatories can be more confident the equipment has not been tampered with by either the MC, or a third party.

***

#### 5.2.6. Scheduling the Ceremony
{: .no_toc }
The key generation that takes place during the setup ceremony is the most sensitive part of the Cerberus protocol, hence the need to formalise the process.

##### 5.2.6.1. Identify a suitable venue
{: .no_toc }
Why we recommend certain features of the setup ceremony venue:
* **A table for least five people:** sufficient space for three signatories plus a setup station and equipment.  
* **At least one wall with no windows or glass walls:** You want to avoid the chance of anyone peering in over the shoulders of signatories as they generate their keys and record the seed phrase.  
* **No security cameras installed:** Any camera recordings that capture PINs or seed phrases could be later used by third parties to compromise the Cerberus storage.
* **A minimum of three power points close to the table:** Running out of power at a critical moment will waste signatories' time.
* **A waste paper basket:** You're going to be throwing a little non-sensitive paper-based stuff away.
* **Access to good coffee:** Caffeine to keep everyone alert and focused.

We recommend keeping the purpose of the booking secret to minimise the chances that:
1) a third party learns who the organisation's bitcoin storage signatories are;
2) a third party learns of the ceremony and takes steps to compromise the room in advance of the ceremony taking place (e.g. installing a hidden camera).

##### 5.2.6.2. Establish a suitable time and date
{: .no_toc }
Yes, the ceremony may take five hours. We expect it can be done much faster if everyone is properly prepared and has already run through the protocol, but signatories should be prepared for longer in case something goes wrong and need to be repeated.

##### 5.2.6.3. Book the venue
{: .no_toc }
N/A

##### 5.2.6.4. Invite the signatories
{: .no_toc }
N/A

***

#### 5.2.7. Preparation Checks
{: .no_toc }

##### 5.2.7.1. Confirm receipt of online purchases**
{: .no_toc }
N/A

##### 5.2.7.2. Double-check that each signatory has completed their tasks**
{: .no_toc }
N/A

