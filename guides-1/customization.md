# Customization

The connectivity SDK can be visually customized for an improved end user experience.

## Setting the application DID

Each dApp needs to generate its own DID, called the application DID. This can be done with any identity wallet (ie: Elastos Essentials through the "Developer mode" menu) able to generate a DID. Then, the dApp can let the connectivity SDK know what is its DID. By doing so, identity wallets can customize their screens to display dApp information, for example when getting credentials from users.

{% hint style="info" %}
After creating the application DID in an identity wallet, you may also want to set an avatar and proper name for it, as this is what is used by identity wallets to inform users of the requesting dApp.
{% endhint %}

{% tabs %}
{% tab title="Typescript" %}
```typescript
import { connectivity } from "@elastosfoundation/elastos-connectivity-sdk-js";

connectivity.setApplicationDID("did:elastos:your-app-did");
```
{% endtab %}
{% endtabs %}

## Using a different UI handler

When several connectors are registered, the connectivity SDK first shows a prompt to let users choose which connector to use for connectivity operations. This prompt has its own UI style that dApps may like or not.&#x20;

dApps can choose to build their own UI by providing a custom UI handler like this:

{% tabs %}
{% tab title="Typescript" %}
```typescript
import { connectivity } from "@elastosfoundation/elastos-connectivity-sdk-js";

// "yourHandler" must implement the IGenericUIHandler interface, 
// and the showConnectorChooser() method that should display the UI
// prompt and return the selected connector name as a result.
connectivity.setGenericUIHandler(yourHandler);
```
{% endtab %}
{% endtabs %}

## Using dark mode

In case your dApp chooses to use the default UI (for instance, the connector prompt described above), the dark mode can be applied by calling the following method from the theme service:

{% tabs %}
{% tab title="Typescript" %}

```typescript
import { theme } from "@elastosfoundation/elastos-connectivity-sdk-js";

theme.enableDarkMode(true);
```
{% endtab %}
{% endtabs %}

## Language configuration

English, French and Mandarin Chinese are the three languages currently provided by default by the connectivity SDK. They are used by the connector prompt mostly. It is also possible to add new languages, force the used language, or translate some strings using the following methods:

{% tabs %}
{% tab title="Typescript" %}

```typescript
import { localization } from "@elastosfoundation/elastos-connectivity-sdk-js";

localization.addLanguage("it", [
  "item": "Translation"
]);
localization.setLanguage("it");
let translated = localizatiion.translateInstant("item");
```

{% endtab %}
{% endtabs %}

****

****

****
