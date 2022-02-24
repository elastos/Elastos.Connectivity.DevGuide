# The Essentials Connector

The **Elastos Essentials connector** allows your dApp to communicate with the Elastos Essentials wallet to do identity and other operations (in addition to crypto operations).

Quick start:

{% tabs %}
{% tab title="Javascript" %}
```
npm i @elastosfoundation/essentials-connector-client-browser
```



```typescript
import { connectivity } from "@elastosfoundation/elastos-connectivity-sdk-js";
import { EssentialsConnector } from '@elastosfoundation/essentials-connector-client-browser';

const essentialsConnector = new EssentialsConnector();
connectivity.registerConnector(essentialsConnector);
```
{% endtab %}
{% endtabs %}

For more information, please refer to the **Elastos Essentials documentation**.

