# Writing a Custom Connector

The main objective of the connectivity SDK is to let any wallet provide its own connector, in order to give more choices to dApps and end-users. Currently, the Elastos Essentials connector is the first one that was written, but as more wallet apps supporting this SDK will emerge, related connectors will be provided as well.

Connectors must implement a specific interface from the connectivity SDK and be deployed as standalone libraries that developers can install.&#x20;

Implementing a new connector is rather straightforward:

{% tabs %}
{% tab title="Typescript" %}
```typescript
import { Interfaces } from "@elastosfoundation/elastos-connectivity-sdk-js";

export class YourConnector implements Interfaces.Connectors.IConnector {
    // Implement methods such as issueCredential(), signData(), pay().
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
As the connectivity SDK connector interface evolves, please directly refer to the latest interface version in the connectivity SDK source code, from your favorite code editor. You can also refer to the Essentials Connector implementation for reference.
{% endhint %}
