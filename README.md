# Introduction

In a decentralized environment, while end-users are responsible for holding their identity and funds, most applications are not centrally hosted on a single server (the developer's) but **need to rely on a wallet** chosen by users.

The most common example of this is when Ethereum applications run on web apps - they **all rely on MetaMask** to facilitate certain wallet operations, such as publishing transactions.

In the Elastos world, it's no different - the only exception is that, in addition to wallet operations, Elastos also uses the "wallet app" to manage users' decentralized identities and other services.

These operations are usually provided by another application, the **"wallet"** which hosts users' identities and **Connectivity SDK** (and its connectors) **that** **acts as a bridge between third-party and wallet applications**.

## Elastos Connectivity SDK

The Connectivity SDK provides an easy-to-use interface for all operations that require user interaction in a wallet app, such as retrieving DID credentials, calling smart contracts, or authenticating on an Elastos Hive provider in order to manage data storage.

This SDK provides a **flexible architecture** and **custom** **connectors** that implement the Connectivity SDK interface so it can be dynamically added. Currently, the two recommended connectors are the **Elastos Essentials connector** (which implements communications between apps and the Elastos Essentials wallet) and the **Local Identity Connector** (an embedded connector that manages only very simple operations to more easily onboard new users).

#### TODO external link to the Elastos Essentials connector for reference

{% content-ref url="connectors/local-identity-connector.md" %}
[local-identity-connector.md](connectors/local-identity-connector.md)
{% endcontent-ref %}



##
