# A nice "Connect wallet" flow

Even without talking about the connectivity SDK, many Web3 dApps - including popular ones - still struggle to provide the perfect "connect wallet" experience for their DeFi projects.

You will sometimes see "connect with Metamask" when you are in a mobile wallet built-in browser (which doesn't make sense, and actually means "use the injected provider"). Or "Wallet connect", when you are in a built-in browser as well (which also doesn't make sense, as built-in browsers use injected web3 providers, they don't need wallet connect).

To try to help you as a dApp developer, here is a suggested pseudo-algorithm to let your app decide what should be shown when.

### Use case 1: Optional DID, mandatory crypto address

If your dApp needs users to provide a EVM address (ethereum compatible) and a DID, but it can live without a provided DID:

```typescript
if (mobile) {
  if (window.ethereum) {
    // you are in a mobile wallet
    if (window.elastos) {
      // The mobile wallet has DID / elastos capabilities (Essentials)
      // -> show "Sign in with DID" -> calls connSDK.requestCredentials() -> after connection, use connectivity.getActiveConnector().getWeb3Provider() to access ethereum commands
    }
    else {
      // The mobile wallet has no elastos capability (token pocket, trust wallet, MM mobile)
      // -> show "You cannot use DIDs" (because mobile wallets usually intercept the wallet connect requests and keep them for themselves)
      // -> show "Connect" (this will use the injected window.ethereum for ethereum transactions)
    }
  }
  else {
    // You are in a standard mobile browser like chrome or safari mobile
    // -> show "Sign in with DID" -> calls connSDK.requestCredentials() -> the conn sdk will use wallet connect and sign in with DID -> after connection, use connectivity.getActiveConnector().getWeb3Provider() to access ethereum commands
    // -> show "Wallet connect" -> any mobile wallet can be used. But this will bind the eth address only, not the DID
  }
}
else {
  // Desktop
  if (window.ethereum) {
    // MM plugin is installed
    // -> show "Sign in with DID" -> calls connSDK.requestCredentials() -> the conn sdk will use wallet connect and sign in with DID -> after connection, use connectivity.getActiveConnector().getWeb3Provider() to access ethereum commands
    // -> show "Connect" (this will use the injected window.ethereum for ethereum transactions)
  }
  else {
    // no crypto plugin
    // -> show "Sign in with DID" -> calls connSDK.requestCredentials() -> the conn sdk will use wallet connect and sign in with DID -> after connection, use connectivity.getActiveConnector().getWeb3Provider() to access ethereum commands
    // -> show "Wallet connect" -> any mobile wallet can be used. But this will bind the eth address only, not the DID
  }
}
```

### Use case 2: crypto address only, no connectivity SDK

For your reference as well as for comparison of the 2 use cases, even if this is not part of the connectivity SDK, here is the flow f your dApp needs users to provide only an EVM address (Ethereum compatible):

```typescript
if (mobile) {
  if (window.ethereum) {
    // you are in a mobile wallet
    // -> show "Direct connect" (this will use the injected window.ethereum for ethereum transactions)
  }
  else {
    // You are in a standard mobile browser like chrome or safari mobile
    // -> show "Wallet connect" -> any mobile wallet can be used.
  }
}
else {
  // Desktop
  if (window.ethereum) {
    // MM plugin is installed
    // -> show "Direct connect" (this will use the injected window.ethereum for ethereum transactions)
    // -> show "Wallet connect" -> any mobile wallet can be used.
  }
  else {
    // No crypto plugin on the desktop browser
    // -> show "Wallet connect" -> any mobile wallet can be used.
  }
}
```

### Don't forget to use the right web3 instance after connection

Here is a code that shows how to avoid common developers mistakes, who are used to use "window.ethereum" and are sometimes confused when web3 provider instances coming from other locations are involved:

```typescript
let web3;

connectPopup() {
  doConnectionProcess();
  if (connectedThroughInjectedWeb3)
    web3 = window.ethereum;
  else {
    // Case 1: if using the connectivity SDK
    web3 = connectivity.getActiveConnector().getWeb3Provider();
    // Case 2: if using wallet connect directly
    web3 = [Your wallet connect provider];
  }
}

// Example of further call to the web3 instance
getBalance() {
  web3.getBalance(); // DO
  window.ethereum.getBalance() // DON'T
}
```

### Wallet connect connectivity issues

When adding a "connect with wallet connect" button in your dApp, it's advised to always kill the current wallet connect session first, to force a new connection. This is particularly useful in case the remote wallet app and the dApp get disconnected or desynchronised somehow.&#x20;

By killing the session, this gives a "fresh start" to the wallet connect connectivity.
