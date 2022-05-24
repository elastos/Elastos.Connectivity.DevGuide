# The built-in connector standard

## The Javascript window.elastos instance

In **javascript** environments (using the Connectivity SDK JS), **mobile wallets** supporting Elastos features - such as Elastos Essentials - define the global **window.elastos** instance in their in-app browser, similarly to window.ethereum used to inject ethereum Web3 providers.

### window.elastos replaces other connectors

When window.elastos is defined (injected by the parent native browser or plugin), **the connectivity SDK uses it automatically**. Other connectors added by dApps are not used in such case.&#x20;

### window.elastos is not window.ethereum

If you are used to write ethereum web3 apps, you may have used window.ethereum as a web3 instance to execute ethereum requests.

Elastos' window.elastos is similar, but used to pass Elastos specific commands such as DID credential requests (eg: requestCredentials(), to "sign in with DID")

When a dApp is running inside a mobile wallet application such as Elastos Essentials, both window.ethereum and window.elastos are defined.

### How to detect if we are in a specific built-in browser?

{% tabs %}
{% tab title="Javascript" %}
```typescript
// We are in the "Essentials" browser
if (window.elastos.name === "essentialsiab") {
 ...
}
```
{% endtab %}
{% endtabs %}
