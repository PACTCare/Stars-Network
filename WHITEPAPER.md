<img src="https://github.com/PACTCare/Stars-Network/blob/master/images/stars_network.png" width="400px">

**A Vision of a Distributed, Free and Collectible Web**

Draft 0.1, May 2019, [David Hawig](https://github.com/Noc2), [PACT Care B.V.](https://pact.care/)

_If you want to help either join our **[discord server](https://discord.gg/VMj7PFN)** or you can open an issue. You can also submit pull requests to this repository._

## Table of Contents

- [Abstract](#abstract)
- [Introduction Shooting for the Stars](#introduction)
  - [Components](#components)
  - [Hypotheses](#hypotheses)
- [Network Space, the final frontier](#network)
  - [Starlog Substrate](#starlog)
  - [Captain's Log BigchainDB](#captain)
  - [Starspace – IPFS](#starspace)
  - [Starbridge WebSocket Client](#starbridge)
- [Incentive Stars](#incentive)
- [Governance The Federation](#governance)
- [Conclusion](#conclusion)
- [Citations](#citations)

## Abstract

Web 3.0 (aka distributed web) currently suffers from a lack of distributed metadata which leads for example to non-userfriendly identifiers, copyright problems and siloed data. This paper introduces the Stars Network, which tries to overcome these issues by creating a distributed and decentralized metadata storage.

As an initial setup, the Stars Network uses a Proof-of-Stake blockchain/smart contract layer based on Substrate, a Proof-of-Authority database layer based on BigchainDB, and a peer-to-peer storage network based on IPFS. This network can however be easily connected to other distributed ledgers and use different databases and storage layers. Additionally, it complies with GDPR and provides a first step to fulfill the EU Copyright Directive, at least to a technically possible and reasonable degree. 

**The paper itself is under active development and represents a research project. It is neither intended to be a final design nor a product specification.** 

<h2 id="introduction">
  Introduction – Shooting for the Stars
</h2>

_“The Web as I envisaged it, we have not seen it yet.” Tim Berners-Lee_

It’s without question that the World Wide Web is constantly evolving. The current interactive Web 2.0 faces multiple problems, when it comes to trust, censorship, and distribution. The distributed web sometimes also referred to as Web 3.0 or DWeb is based on verifiability and offers potential solutions for these problems [\[1\]][1]. 

Although the next generation of web offers many benefits, it currently still faces multiple challenges. For example:
* Mandatory Ownership: In most distributed ledger system a key requirement is to own the tokens of the network to participate. 
* Incentive structure: Often network providers are either not incentivized at all or are incentivized for providing unnecessary services. 
* Scalability: Fully distributed applications can’t compete with the scalability of centralized applications. 

Additionally, the distributed web should try to overcome existing problems of the current web, like
* Data Silos: Distributed systems often lead to distributed and unconnected data silos or rely on centralized authorities, to implement searchability and accessibility.
* Copyright: Distributed networks are currently mostly used for copyright infringement and don’t provide a clear ownership structure. 

Therefore, users lose complete control over their content.  
This paper tries to address these issues to a certain degree by combining multiple existing technologies. The key technologies behind it are IPFS [\[2\]][2], BigchainDB [\[3\]][3], and Substrate [\[4\]][4].
The network itself fulfills GDPR compliance, specifically the “right to be forgotten,” as well as offers a potential non-governmental solution for relatively clear copyright abuses [\[5\]][5]. 

### Components

The Stars Network is based on the following components:

- **Starlog**: interoperable blockchain/smart contract layer (the reference implementation is based on Substrate)
- **Captain's Log**: an immutable and distributed metadata database (the reference implementation is based on BigchainDB)
- **Starspace**: a distributed storage layer (the reference implementation is based on IPFS)
- **Starbridge**: an event-based connection of the different layers (the reference implementation is based on a WebSocket connection)
- **Star**: the network token and voting power
- **Federation**: the governance structure of the network

### Hypotheses 

This paper is based on three hypotheses and the resulting design principals. The assumptions aren’t proven facts and therefore open for discussion. 

**A distributed web - The world wide web should be diverse and distributed.** That’s why all systems should try to archive interoperability and distribution. Additionally, if it’s possible rather than finding one single truth for everyone, users should themselves decide who to follow, in which cluster to participate, etc. This hypothesis is also based on the macroeconomic assumption that the capabilities of monopolies or oligopolies reduce efficiency compared to the perfect competition [\[6\]][6]. The internet in its current state has multiple monopolies or oligopolies in different areas. For example, Google has a market share of above 90% [\[7\]][7] and quarterly earnings of above 30 billion dollars [\[8\]][8]. This is not only economically inefficient but also increase the chance of censorship [\[9\]][9] and search bias [\[10\]][10]. Therefore, the first goal is to create a distributed and diverse network. 

**A free web - The internet should be free, open and accessible for everyone.** It means paying for content or the requirement to log in should be optional in as many cases as possible. For example, the access to information shouldn’t require specific tokens, credit cards or accounts. Although network neutrality often doesn’t fulfill this hypothesis, the internet itself and websites generally try to be easily accessible and open. However, the next generation of the web has a lot of problems in this space. It’s often a key requirement to download additional software, own something related to the protocol to use it or pay for transactions. Another goal of this paper is therefore to overcome these challenges. 

**A collectible web - Users should be able to own, collect and be responsible for their digital content and data.** This whitepaper assumes that striving to achieve greater ownership of wealth is one of the driving factors behind human technological advancement. Therefore, digital content needs to be ownable and tradable. The discussion around the European copyright directive shows that the current system has multiple flaws, which need to be addressed. For example, once data is uploaded on the current version of the web users and companies quickly lose control over their data. Important to note here is that the ownership of digital data should be an optional requirement, which means users should still be able to create content completely anonymous. 

<h2 id="network">
  Network – Space, the Final Frontier
</h2> 

The network itself consists of a blockchain/smart contract layer called Starlog, an immutable and distributed database layer called Captain's log and a distributed storage layer called Starspace. By splitting the technology stack into different layers, each layer can be adapted according to their key requirements. For example, it is important that the Starlog layer has a high level of distribution and only handles the most important information. Therefore, the Captain's log can take care of the metadata more efficiently and has lower distribution requirements. 

<img src="https://github.com/PACTCare/Stars-Network/blob/master/images/stars_network_1.png" width="310px">

To create a distributed and interoperable web, every layer can be replaced with different technologies, which also leads to unlimited scalability of the network. The image below shows different examples and how the layers might connect. 

<img src="https://github.com/PACTCare/Stars-Network/blob/master/images/stars_network_2.png" width="550px">

Different Starlog layers can connect via bridges. Starlog itself stores Decentralized Identifiers (DIDs) [\[11\]][11], which can point to different database layers and the metadata itself can point to different storage locations. Below, a reference implementation for each layer is presented. 

<h3 id="starlog">
  Starlog – Substrate 
</h3>

Substrate is an open source framework by Parity Technologies to develop blockchains in rust. It can connect via so-called bridges and parachains to enable a future multichain network. This framework enables a diverse and scalable web, in which all kinds of distributed hosted applications use smart contracts or simple runtimes. Additionally, it includes upgradability right from the start, without the necessity of hard forks and makes use of the hybrid GRANDPA (GHOST-based Recursive ANcestor Deriving Prefix Agreement) and BABE (Blind Assignment for Blockchain Extension) consensus algorithm. BABE is the block production mechanism that determines the producer of new blocks. GRANDPA combines probabilistic, Proof-of-work-like finality with byzantine provable finality [\[12\]][12]. In GRANDPA, validators vote for blocks at different heights. As soon as a block has more than 2/3 of the votes this block becomes part of the chain. If there are different parts of the chain, people follow the chain which has more then 2/3 of the vote, so in the image the chain on the bottom. 

<img src="https://github.com/PACTCare/Stars-Network/blob/master/images/grandpa.png" width="400px">

This paper suggests implementing Starlog as a parachain of Polkadot, which allows an easy connection to a wide variety of blockchain projects. Additionally, a Parachain profits from the shared security of the relay chain.

Since Starlog stores data entries permanently and based on a network consensus, it keeps track of the most important information only. This information includes:

* DID
* Unique name
* License code
* Storage location
* Timestamp

The DID points to the metadata storage. For example, the following string represents a valid Starlog DID: 

_did:bcdb:0b51b44e0330995979a5ddaa206260b1c18e2471ad51043c27d68d8a9c40261f_

The prefix “did” stands for decentralized identifier and “bcdb” means “BigchainDB”. The rest of the DID is the BigchainDB transaction id of the first metadata upload, which is a SHA3-256 hash of the transaction. This hash can be used to track all future update to the metadata entry on BigchainDB. A similar system could, for example, be implemented with IOTAs Masked Authenticated Messaging (MAM). 

Starlog allows users to register unique names similar to domain names, which can be combined with the metadata. The concept behind the names and the DIDs is based on the Ethereum Non-fungible Token Standard. Because of this, every Starlog DID and name entry is unique and, therefore, collectible as well as tradable. The Substrate chain also stores the ownership rights and the content license in the form of a numeric license code, which also allows to log delete requests for owned content publicly. As a result, each number of the license code represents a specific license state. This system allows content creators to provide signed information about the usage rights of their work. Thus, enabling a technical possible solution for the EU Copyright Directive and GDPR compliance. 

The storage location provides the location of an initial permanent storage provider, which ensures the availability of a file in a distributed network.  The main benefit of the timestamp is to provide a trusted timestamping service for all kinds of digital content. This can, for example, be useful to prove the existence of certain documents. 

Furthermore, Starlog stores all government activities as well as token movements. Users sign all uploaded Starlog entries and therefore own these uploads. However, if they don’t share the specific public key others won’t know the owner of the data. 

To connect the above interaction with the other layers of the Stars Network, the on-chain interaction fires certain events, which are then handled by the Starbridges (see Starbridge: WebSocket Client). 

Additionally, Starlog provides a layer for smart contracts, which could potentially enable in the future multiple services around digital content. This can, for example, be used to develop content marketplaces for the stored unique information or to provide storage/hosting smart contracts based on the DIDs and the storage location. This essentially represents an alternative to systems like Filecoin. Smart contracts for Substrate can be developed with the ink! CLI. 

<h3 id="captain">
  Captain's Log – BigchainDB
</h3>

BigchainDB is a database with blockchain characteristics, like immutability and Byzantine Fault Tolerance. This means up to a third of the nodes can fail in any way, and the system continues to work. The key requirement for BigchainDB is that not everyone can set up an arbitrary number of nodes. Instead, it’s required that nodes are only hosted by a so-called “BigchainDB consortium”, in which different elected and know-authorities run the nodes. For the Captain's Log this distribution is archived by the Substrate-based governance (see Governance: Federation). A benefit of using BigchainDB compared to a regular blockchain is that every element of the metadata is easily and directly searchable, without the requirement of additional services. Moreover, Substrate nodes aren’t optimized for data querying and, constant requests could cause issues with the performance of the nodes. This is one of the reasons, why the Captain's Log stores certain redundant information. Furthermore, the interaction with the BigchainDB is free and doesn’t require a user to own something specific to the network, like a token, to create a metadata entry. 

The database layer essentially stores Decentralized Identifiers Documents (DDOs). A DDO document is composed of standard DDO attributes like:

* @context: 
* Id
* authentication
* service

The service entry contains the metadata as well as validation entries. A service entry contains the following components:

* type: CaptainsMetadata
* serviceEndpoint
* metadata

And the metadata contains the following elements:

* hashes
* title
* description
* filetype
* thumbnail
* similarity digest

The similarity digest is a context sensitive hash, which allows the comparison of two different hashes to obtain an estimate of the degree of similarity between the two documents. This is especial helpful for find near duplicates of documents for search engines. Additionally, the metadata also stores the following information, which is already stored on-chain:

* unique name
* license code
* storage location

The complete data allows for example for decentralized searchability, verifiability, near-duplicate detection and the combination of address- and name-based storage. Every Captain’s Log metadata entry must include a unique file hash, which points to a file stored on Starspace. 

Since one of the key assumptions of the paper is distribution and diversity, the Captain’s Log provides location-based links as well as a name-based addresses. This means content can be found via names in the form of hashes and via the current web addresses. The combination of both has proven in the project Dweb.page to be a successful way to ensure fast initial loading speed as well as additional network distribution of content [\[13\]][13]. The following picture shows the concept. 

<img src="https://github.com/PACTCare/Stars-Network/blob/master/images/ipfs.png" width="550px">

The user number 1 requests a file from user number 3 via a location-based request (http://www...) as well as a name-based (Qm…) request to the network. Since the file is not yet distributed the traditional way loads the file faster. User number 2 recognizes the interest in the file and decides to load this file as well. Now, when user number 4 request this file in the same way as user number 2, he or she receives it via the named-based system from his neighbor number 2. 

Apart from the above information, the metadata layer also stores availability and validation data. This is essentially data provided by other people than the publisher, which describes the uploaded content in more detail. The availability data helps to provide information about the availability of content in a distributed network. This is essential in cases where no one provides a permanent storage for uploaded content. The data validation is essentially a trust layer, in which different persons can rate the quality of the provided data. 

Rather than trying to find one single truth directly on the blockchain (e.g., token-curated registry), the metadata system uses a subscription-based system on the Captain’s Log (see image below). Reasons for this are the expected high frequency of changes and updates to the metadata as well as the different interests when it comes to search-topics.

<img src="https://github.com/PACTCare/Stars-Network/blob/master/images/captainslog.png" width="600px">

This means that content publishers store immutable metadata and unavailability data on the chain. Consumers can then decide which publishers (signatures) they trust and follow. In practice, this will be automatically archived by rules hard-coded into the interface (e.g., dweb.page). The benefit of the system is the immediate availability of information without the requirement of an additional voting system nor a filtering system, which takes individual preferences into account. In case it’s requested, a token-curated register or something similar can at any time be implement as smart contract on the Starlog layer.  

<h3 id="starspace">
  Starspace – IPFS
</h3>

In comparison with the previous layers, the Starspace stores every kind and size of data. Therefore, Starspace uses IPFS as the initial underlying technology layer. However, the metadata system can easily support other protocols and their respective interoperability. IPFS is a protocol to create a content-addressable, peer-to-peer method of storing data.

Starspace only stores information based on individual requests. Thus, information can also be deleted if the license code on Starlog is changed and the event-based system triggered. The distribution of content on the Starspace network is also depended on this license code. For example, it’s possible to specify that data should be only stored on one location and not distributed in the network. This way the setup is GDPR compliant.

<h3 id="starbridge">
  Starbridge – WebSocket Client
</h3>

Starlog talks to other layers via an event-based system, which is triggered based on specific chain events. For example, in case a user logs a delete request on Starlog, it needs to be ensured that the specific Captain’s Log and Starspace also receive this information. The Starbridges subscribe to these events via a WebSocket connection and ensure the appropriate action on the storage or metadata layers. Different Starbridges are hereby responsible for different block numbers. Once the update is executed, they log the result after a certain time on Starlog. The result can also be an unsuccessful execution. If this is the case or if the log entry doesn’t appear at all, the next Starbridge takes care of the job. 

<img src="https://github.com/PACTCare/Stars-Network/blob/master/images/starbridge.png" width="550px">

To calculate the probability for firing an event when a certain Starbridge is currently unavailable, this paper assumes that the probability that a Starbridge operates without failure for a time t is given by the following equation based on the paper by Jaynes, E. T., 1976 `Confidence Intervals vs. Bayesian Intervals'. [\[14\]][14] 

<img src="https://github.com/PACTCare/Stars-Network/blob/master/images/math1.PNG" width="250px">

λ is, in this case, the unknown "rate of failure". With this you can derive the following equation for the probability for hitting the system when it’s unavailable [\[15\]][15]:

<img src="https://github.com/PACTCare/Stars-Network/blob/master/images/math2.PNG" width="400px">

Where TU is the "uptime" and TD is the "down time", in seconds. θ is the time of the first downtime (in seconds) observed by the user and F is the expected number of "downtime periods". This equation shows that if Starbridge providers ensure high availability, the probability that an available honest provider didn’t get an event gets quickly close to zero. Especially if there are multiple rounds by different Starbridge providers. 

<h2 id="incentive">
  Incentive – Stars
</h2>

The monetary token and voting power of the network is called Star. All monetary transactions in the network, like paying for unique names, fees or participating in smart contract marketplaces require Stars as a payment token. However, the goal is to make it as easier as possible to use other currencies for payment. Therefore, systems like Chainlink will be implemented in a later stage to make it even possible to use fiat for buying digital goods without trusting a centralized authority. The ability to exchange different currencies almost instantly makes it unnecessary to implement a two-token system, in which a stable coin is used for monetary transactions, and another token is used for staking. 

It’s important to notice that pure metadata transactions on the Captain’s Log don’t require any payment. This way it’s ensured that people don’t need to own anything to participate in the network and to share their metadata. Only if they want to trade their data, own a unique name, vote for network participants or have an additional level of security, the participation in the network is required. 

<h2 id="governance">
  Governance – The Federation 
</h2>

Without a proper governance structure right from the start, a network like this would be unable to adapt to future developments or split into different systems that represent different opinions (see Bitcoin Forks). The government of the Stars Network is called Federation and is based on Proof-of-Stake system. All Stars holders are part of the Federation, which means they have the right to vote for a Captain’s Log, Starbridge provider or specific network-related suggestions. Voting is incentivized by an inflation rate, which means that the ones participating in the voting process will receive an appropriate share of new Stars. Voting takes place infrequently, and the Star tokens need to be staked to participate in the voting process. In the case of voting for malicious parties the staked Star tokens are lost.

Similar Captain’s Log and Starbridge provider need to put a certain number of tokens at stake to be listed as potential candidates. If they get successfully elected and act malicious, they will lose all their staked tokens. This is especially important for the proof-of-authority based Captain’s Log setup, where a system which only puts the identity at stake might not be a sufficient incentive to deliver the most secure network. [\[16\]][16]  

In general, the Star Network is able to store transaction in a clear and legally binding way. But, at the same time, it can also be used under complete anonymity. Knowing that legally binding contracts are sufficient in a lot of use cases, the first iteration of the Stars Network will focus on supporting these legal structures. Let’s take the example of a delete request. Normally, changing the license code on Starlog would automatically delete the related content on Starspace. However, a malicious party might suppress a successful execution of this request. But since the malicious party, as well as the request, are publicly immutable logged, it’s easy to take appropriate steps to sue the specific persons or legal entity. 

Another example of this legal application are hash-based ownership rights. At this point, Starlog only provides the necessary, immutable infrastructure for a centralized, publicly auditable marketplace to integrate the tradability of digital goods and implement the necessary authentication layers. The reason for this is that the provided hashes and similarity digest don’t provide clear information to decide, on-chain, the difference between new content and copied content, since an authentication service is a key requirement.  At a later stage, it might be possible to fully decentralize these systems based on decentralized authentication services.  

## Conclusion

This paper presents a first version of a distributed and decentralized metadata system, which tries to achieve high distribution, free accessibility, and collectability for digital content. 

## Citations

[1]: https://www.theguardian.com/technology/2018/sep/08/decentralisation-next-big-step-for-the-world-wide-web-dweb-data-internet-censorship-brewster-kahle
[2]: https://ipfs.io/
[3]: https://www.bigchaindb.com/
[4]: https://www.parity.io/substrate/
[5]: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32001L0029 
[6]: https://books.google.de/books?id=JpuDoMDX4tsC&pg=PA218&redir_esc=y#v=onepage&q&f=false
[7]: https://www.statista.com/statistics/216573/worldwide-market-share-of-search-engines/
[8]: https://www.statista.com/statistics/267606/quarterly-revenue-of-google/ 
[9]: https://www.theguardian.com/technology/2018/nov/27/google-employees-letter-censored-search-engine-china-project-dragonfly
[10]: https://techcrunch.com/2018/02/09/google-fined-21-1m-for-search-bias-in-india/?guccounter=1&guce_referrer_us=aHR0cHM6Ly90ZWNoY3J1bmNoLmNvbS8&guce_referrer_cs=trGdiLkoRxbYgTF1EG6m8w
[11]: https://w3c-ccg.github.io/did-spec/
[12]: https://github.com/w3f/consensus/raw/master/pdf/grandpa.pdf 
[13]: https://github.com/PACTCare/Dweb.page
[14]: http://bayes.wustl.edu/etj/articles/confidence.pdf 
[15]: https://stats.stackexchange.com/questions/6636/probability-calculation-system-uptime-likelihood-of-occurence
[16]: https://medium.com/@timdaub/why-you-shouldnt-ship-to-a-poa-network-7e2b5aa83aa9


* [1] Dweb: https://www.theguardian.com/technology/2018/sep/08/decentralisation-next-big-step-for-the-world-wide-web-dweb-data-internet-censorship-brewster-kahle
* [2] IPFS: https://ipfs.io/
* [3] BigchainDB: https://www.bigchaindb.com/
* [4] Substrate: https://www.parity.io/substrate/
* [5] Directive 2001/29/EC: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32001L0029 
* [6] Economics: A Contemporary Introduction: https://books.google.de/books?id=JpuDoMDX4tsC&pg=PA218&redir_esc=y#v=onepage&q&f=false
* [7] Market share search engines: https://www.statista.com/statistics/216573/worldwide-market-share-of-search-engines/
* [8] Revenue of Google: https://www.statista.com/statistics/267606/quarterly-revenue-of-google/
* [9] Google employees sign letter against censored search engine: https://www.theguardian.com/technology/2018/nov/27/google-employees-letter-censored-search-engine-china-project-dragonfly
* [10] Google fined for search bias: https://techcrunch.com/2018/02/09/google-fined-21-1m-for-search-bias-in-india/?guccounter=1&guce_referrer_us=aHR0cHM6Ly90ZWNoY3J1bmNoLmNvbS8&guce_referrer_cs=trGdiLkoRxbYgTF1EG6m8w
* [11] Decentralized Identifiers: https://w3c-ccg.github.io/did-spec/
* [12] GRANDPA: https://github.com/w3f/consensus/raw/master/pdf/grandpa.pdf 
* [13] Dweb.page: https://github.com/PACTCare/Dweb.page
* [14] Confidence Intervals vs. Bayesian Intervals: http://bayes.wustl.edu/etj/articles/confidence.pdf 
* [15] Probability calculation, system uptime, likelihood of occurence: https://stats.stackexchange.com/questions/6636/probability-calculation-system-uptime-likelihood-of-occurence
* [16] Why you shouldn’t ship to a POA network: https://medium.com/@timdaub/why-you-shouldnt-ship-to-a-poa-network-7e2b5aa83aa9
