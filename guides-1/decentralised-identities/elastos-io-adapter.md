# Elastos IO adapter

For some operations, the DID SDK requires a **DID adapter** to be a provider. A DID adapter is basically a single method, that can query the Elastos Identity blockchain in order to retrieve DID Document, or Verifiable credentials.

For convenience, the connectivity SDK provides a simple DID adapter, that communicates with the **elastos.io** identity node (service provided by the _gelaxy_ core blockchain team). Of course, dApp developers are free to implement their own custom DID adapters to talk to the identity blockchain node or their choice instead of using this one.

The adapter can be instantiated like this:

{% tabs %}
{% tab title="Typescript" %}
```typescript
import { DID } from "@elastosfoundation/elastos-connectivity-sdk-js";

// Mainnet
let adapter = DID.ElastosIODIDAdapter(DID.ElastosIODIDAdapterMode.MAINNET);

// Testnet
let adapter = DID.ElastosIODIDAdapter(DID.ElastosIODIDAdapterMode.TESTNET);
```
{% endtab %}
{% endtabs %}
