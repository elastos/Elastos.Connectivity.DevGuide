# Ethereum

Because some connectors such as the Elastos Essentials connector implement not only the Elastos connectivity methods, but also standard EVM-compatible Web3 operations (crypto operations, inherited from ethereum), applications also need a way to easily access EVM features.

In the case of the Elastos Essentials connector, the third party **Wallet Connect** library is used to let applications communicate with the wallet seamlessly. In the future, we believe Wallet Connect will be used by most decentralised applications, as it represents a convenient way to let 2 remote applications talk to each other, and fulfills desktop-mobile as well as mobile-mobile use cases.

The connectivity SDK provides access to possibly existing web3 providers used by connectors, so that applications can share those providers. For instance, if a connector uses Wallet Connect for DID operations, users have to scan a QR code to initiate the connection to the identity wallet first. But then, we don't want applications to *also* handle there own Wallet Connect instance just for Web3 EVM operations, as this would require dealing with 2 instances of Wallet Connect, and users to scan QR codes twice. In that regard, the connectivity SDK lets connectors simply **share** their **existing web3 provider** (if they have one) and applications can **reuse** them.

{% tabs %}
{% tab title="Typescript" %}

```typescript
import { connectivity } from "@elastosfoundation/elastos-connectivity-sdk-js";
import Web3 from "web3";

const provider = connectivity.getActiveConnector().getWeb3Provider();
if (provider) {
	const web3 = new Web3(provider);
	const gasPrice = await web3.eth.getGasPrice();
}
```

{% endtab %}
{% endtabs %}
