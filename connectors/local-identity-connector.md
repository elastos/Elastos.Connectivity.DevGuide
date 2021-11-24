# The Local Identity Connector

A local identity connector is available to let users **quick start** using Elastos **without depending on external wallet applications,** such as **Elastos Essentials**. This is useful for several things:

* To **easily onboard new users who don't yet have an external wallet**. A DID can be created for them, and they can get started in the app within a few seconds, then export their DID later on to a real wallet.
* For mobile apps, **to pass the app stores' verification**. iTunes doesn't allow applications to exclusively depend on other applications to run. As a consequence, asking users to "sign in with an external DID wallet" to continue inside an app is forbidden. Because of this, mobile apps willing to be published on iTunes need to use the local identity connector to let users choose whether they want to use a built-in / auto-generated / temporary identity or a real identity from an external wallet, such as Elastos Essentials.

## Basic Flow

What happens when the local identity connector is used in an app?

* **First time only**:
  * User gets prompted for their name.
  * A local DID (in app) is created for them and published to the ID chain
* **When the local identity is already created**:
  * All interactive operations, such as getting DID credentials, **don't leave the initial application**, and fake information is returned. For example, if the application requests the user's email, a fake email such as "[email@nowhere.com](mailto:email@nowhere.com)" is returned by this connector. The reason is that when using local identities, there's no real identity management for users. **It's a simple and temporary way to start using DIDs**. But users may have to quickly start using an external identity wallet to benefit from all the real features.

{% hint style="info" %}
**ALTERNATIVE**: In case applications don't want to integrate the local identity connector, a different way of passing iTunes validation and quickly onboard new users is to let the application generate a temporary DID for users,  maintain their own state to know if a temporary identity is in use, or an external wallet identity is in use, and make sure to not call the connectivity SDK in such situation.&#x20;

This can allow for example to let new users browser some basic app content first, before asking them to create / use their real external identity.
{% endhint %}
