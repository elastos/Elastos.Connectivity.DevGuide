# Manage Connectors

The Connectivity SDK can support several connectors inside the same application so that users can choose the service they want to use. So far, only 2 connectors are available: the **local identity connector**, and the **Elastos Essentials connector**.

{% hint style="info" %}
At least one connector must be provided for each dApp, otherwise connectivity operations cannot be ran. Web dApp usually don't need the local identity connector, while native mobile apps may need it in order to pass the app store review team validation (i.e. iTunes), as app stores do not accept applications that force users to install another application (a wallet) to access the features.
{% endhint %}

## Register a Connector

As seen on the setup page, a connector can be registered like this:

{% tabs %}
{% tab title="Typescript" %}
```typescript
import { connectivity } from "@elastosfoundation/elastos-connectivity-sdk-js";

let essentialsConnector = new EssentialsConnector();
connectivity.registerConnector(essentialsConnector);
```
{% endtab %}
{% endtabs %}

## Force the Active Connector

By default, if multiple connectors are registered, when a user initiates a first connectivity operation, he gets a prompt and needs to choose which connector he wants to use. This is the way to let users choose their wallet or service.

Though, this behavior can be enforced by the dApp by manually setting the active connector like this:

{% tabs %}
{% tab title="Typescript" %}
```typescript
// Set the active connector by its name
connectivity.setActiveConnector(essentialsConnector.name);
```
{% endtab %}
{% endtabs %}

### Get the Active Connector

{% tabs %}
{% tab title="Typescript" %}
```bash
connectivity.getActiveConnector();
```
{% endtab %}
{% endtabs %}

###

