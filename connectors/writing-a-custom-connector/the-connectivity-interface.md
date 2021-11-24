# The Connectivity Interface

The connectivity SDK provides interfaces for the following operations. Those interfaces are implemented by **connectors** such as the **Local Identity Connector** or the **Elastos Essentials connector**.

**TODO: DONT DETAIL TOO MUCH, NO SAMPLE OR API. ONLY PROVIDE THE OP LIST AND EXPLAIN THE BASIC FLOWS**

## Identity (DID) interface

### Getting DID credentials from user's identity

Used to request user's DID string, name, country, or any other information.

{% tabs %}
{% tab title="Typescript" %}
```typescript
export type GetCredentialsQuery = {
    /** JSON Object that holds a list of claims that need to be provided by the user. */
    claims: any,
    /** Optional DID string to which this request must be sent. If provided, the identity wallet must force to select that user's identity. */
    sub?: string,
    /** Can optionally force the DID to be published. If set to false, the identity wallet can allo unpublished DID to return data, but the claling app won't be able to verify the signature. Default: true */
    didMustBePublished?: boolean,
    /** Optional UI customization to match the calling ebsite or app's style. */
    customization?: UICustomization
}

interface IDIDConnectorAPI {
    getCredentials(query: GetCredentialsQuery): Promise<VerifiablePresentation>;
}

```
{% endtab %}
{% endtabs %}

| Feature                    | Summary                                                                                                                                             |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Import DID credentials** | (To let a third party app send a credential to user's profile, so that anyone can query this credential through the get credentials feature later). |
| **Sign data with DID**     | Sign any data with user's DID.                                                                                                                      |

### Ethereum

| Feature           | Summary                                                                            |
| ----------------- | ---------------------------------------------------------------------------------- |
| **Web3 requests** | Handle Web3 ethereum compatible transactions. For instance, a smart contract call. |

### Hive storage

| Feature                        | Summary                                                                                                                                                                                                                                                   |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Issue an app ID credential** | Accessing Hive storages require the identity wallet to confirm that the application is trusted and can access user's storage. This happens through a specific DID credential type and this is done automatically during Hive clients authentication flow. |
