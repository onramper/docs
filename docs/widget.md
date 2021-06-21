# Widget

Here you will find instructions to add the Onramper widget in your website or application. With just a few lines of code, you can allow your users to purchase cryptocurrencies from your web or app.

You can integrate the widget in four different ways:  
· Redirect your users to the widget URL with a referral link. [See more.](#referral-link)  
· Use an iframe or a webview to embed the widget in your application. [See more.](#iframe)  
· Import a component in your React application. [See more.](#react-component)  
· Add it to your static webpage using a CDN import. [See more.](#javascript)

# API Key

To allow users to buy crypto, you need an API key. To get an API key, fill in <a href="https://docs.google.com/forms/d/e/1FAIpQLSdnmTskkGA5QJGjC1eVRcqXZouuGe_ojltlBFs5nFClrSl_gA/viewform?usp=sf_link" target='_blank' >our onboarding form.</a>
Add your API key as a parameter in the URL of the code snippet as follows: `https://widget.onramper.com?apiKey=theAPIkeyyoureceived`.

Note: data retrieved with a test key can be not accurate, for real time prices use a production key.

## Referral link

You can simply add a link to your app or website to redirect users to a page (hosted by us) where the users can buy crypto. The widget url is `https://widget.onramper.com`

If you want to receive a referral fee for every transaction done by users coming from your website, <a href="https://docs.google.com/forms/d/e/1FAIpQLSdnmTskkGA5QJGjC1eVRcqXZouuGe_ojltlBFs5nFClrSl_gA/viewform?usp=sf_link" target='_blank' >fill in our onboarding form to receive your API key</a> and then add your API key to the link as follows: `https://widget.onramper.com?apiKEY=theAPIkeyyoureceived`.

###### HTML code snippet

```html
<a href="https://widget.onramper.com?color=1d2d50" target="_blank">
  Buy cryptocurrencies
</a>
```

###### Live example & customization

Easily customize the buy-page by changing the URL with the [available URL parameters.](#url-parameters)

Redirect customization examples: <a href="https://codesandbox.io/s/onramper-widget-url-redirect-m8tdo" target='_blank' >CodeSandbox</a>

## Iframe

Embed an iframe in your website. This is the easiest way to add the widget on your own page. Just copy-paste the code snippet below in your page. Customize your widget by [adding URL parameters](#url-parameters).

Note: In order to enable the widget for transactions, don't forget to [add your API key](#API-key). In order to enable some features in the widget, don't forget to add the allow attribute to the iframe element.

###### HTML code snippet

```html
<iframe
  src="https://widget.onramper.com?color=346eeb&apiKey=pk_test_x5M_5fdXzn1fxK04seu0JgFjGsu7CH8lOvS9xZWzuSM0"
  height="595px"
  width="440px"
  title="Onramper widget"
  frameborder="0"
  allow="accelerometer;
  autoplay; camera; gyroscope; payment"
  style="box-shadow: 3px 3px 5px 0px
  rgba(0,0,0,0.75);"
>
  <a href="https://widget.onramper.com" target="_blank">Buy crypto</a>
</iframe>
```

###### Live example & customization

<a href="https://codepen.io/thijsmaaslaw/pen/eYzbgXM" target='_blank' >Iframe customization example</a>

#### URL parameters

You can pass some arguments as query parameters to the URL to customize the widget
[For all parameters see CUSTOMIZE section](#customize)

| Name              | Format                                                                   | Example                                                                                                                                                                                                                   | Default value        |
| ----------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| apiKey            | Alphanumeric string                                                      | `?apiKey=yourAPIkey` <a href="https://docs.google.com/forms/d/e/1FAIpQLSdnmTskkGA5QJGjC1eVRcqXZouuGe_ojltlBFs5nFClrSl_gA/viewform?usp=sf_link" target='_blank' >(fill in our onboarding form to receive your API key)</a> | Not set              |
| defaultCrypto     | Cryptocurrency code                                                      | `?defaultCrypto=BTC`                                                                                                                                                                                                      | BTC                  |
| defaultFiat       | Fiat code                                                                | `?defaultFiat=EUR`                                                                                                                                                                                                        | USD                  |
| defaultAmount     | Positive integer                                                         | `?defaultAmount=500`                                                                                                                                                                                                      | 100                  |
| wallets           | Comma-separated list of crypto code:address;memo. Being `;memo` optional | `?wallets=BTC:btcaddr,BNB:binanceAddress;addressTag`                                                                                                                                                                      | Not set              |
| onlyCryptos       | Comma-separated list of crypto codes                                     | `?onlyCryptos=BTC,ETH,NEO`                                                                                                                                                                                                | Not set              |
| excludeCryptos    | Comma-separated list of crypto codes                                     | `?excludeCryptos=BTC,ETH,NEO`                                                                                                                                                                                             | Not set              |
| excludeFiat       | Comma-separated list of fiat codes                                       | `?excludeCryptos=EUR,USD`                                                                                                                                                                                                 | Not set              |
| onlyFiat          | Comma-separated list of fiat codes                                       | `?onlyFiat=EUR,USD`                                                                                                                                                                                                       | Not set              |
| onlyGateways      | Comma-separated list of gateway identifiers                              | `?onlyGateways=Wyre,Moonpay`                                                                                                                                                                                              | Not set              |
| isAddressEditable | Boolean value                                                            | `?isAddressEditable=false`                                                                                                                                                                                                | true                 |
| color             | Hexadecimal color                                                        | `?color=346eeb`                                                                                                                                                                                                           | 31a5ff               |
| fontFamily        | font-family css string                                                   | `Arial, Helvetica, sans-serif`                                                                                                                                                                                            | 'Roboto', sans-serif |

## React component

You can also import the widget as a component in your React application.

###### Installation

```shell
# Using yarn
$ yarn add @onramper/widget

# Using npm
$ npm install @onramper/widget
```

###### Code snippet

```javascript
import OnramperWidget from "@onramper/widget";

export default function WidgetContainer() {
  const wallets = {
    BTC: { address: "btcAddr" },
    BNB: { address: "bnbAddress", memo: "cryptoTag" },
  };

  return (
    <div
      style={{
        width: "440px",
        height: "595px",
      }}
    >
      <OnramperWidget
        API_KEY={apiKey}
        color={defaultColor}
        fontFamily={fontFamily}
        defaultAddrs={wallets}
        defaultAmount={defaultAmount}
        defaultCrypto={defaultCrypto}
        defaultFiat={defaultFiat}
        defaultFiatSoft={defaultFiatSoft}
        defaultPaymentMethod={defaultPaymentMethod}
        filters={{
          onlyCryptos: onlyCryptos,
          excludeCryptos: excludeCryptos,
          onlyPaymentMethods: onlyPaymentMethods,
          excludePaymentMethods: excludePaymentMethods,
          excludeFiat: excludeFiat,
          onlyGateways: onlyGateways,
          onlyFiat: onlyFiat,
        }}
        isAddressEditable={isAddressEditable}
        amountInCrypto={amountInCrypto}
        redirectURL={redirectURL}
      />
    </div>
  );
}
```

###### Live example & customization

While importing the widget as a React component, you can customize it using the component props below.
<a href="https://codesandbox.io/s/onramper-widget-react-component-y3nd1" target='_blank' >CodeSandbox</a>

#### Component props

[For all props see CUSTOMIZE section](#customize)

| Name              | Type                                                                                                                                                              | Example                                                                                                                                                                                                             | Default value        |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| API_KEY           | string?                                                                                                                                                           | `"yourAPIkey"` <a href="https://docs.google.com/forms/d/e/1FAIpQLSdnmTskkGA5QJGjC1eVRcqXZouuGe_ojltlBFs5nFClrSl_gA/viewform?usp=sf_link" target='_blank' >(fill in our onboarding form to receive your API key)</a> | undefined            |
| defaultCrypto     | string?                                                                                                                                                           | `"ETH"`                                                                                                                                                                                                             | undefined            |
| defaultFiat       | string?                                                                                                                                                           | `"EUR"`                                                                                                                                                                                                             | "USD"                |
| defaultAmount     | number?                                                                                                                                                           | `500`                                                                                                                                                                                                               | 100                  |
| defaultAddrs      | object?                                                                                                                                                           | `{"BTC": { address: "btcAddr" },"BNB": { address: "bnbAddress", memo: "cryptoTag" }}`                                                                                                                               | {}                   |
| filters           | An object containing the attributes `onlyCryptos`, `excludeCryptos`, `onlyPaymentMethods`, `excludePaymentMethods`, `excludeFiat`, `onlyGateways` and `onlyFiat`. | `{filters:{onlyCryptos:["BTC", "ETH", "NEO"]}`                                                                                                                                                                      | {}                   |
| onlyCryptos       | string[]?                                                                                                                                                         | `["BTC", "ETH", "NEO"]`                                                                                                                                                                                             | undefined            |
| excludeCryptos    | string[]?                                                                                                                                                         | `["ETH", "NEO"]`                                                                                                                                                                                                    | undefined            |
| onlyFiat          | string[]?                                                                                                                                                         | `["USD", "EUR"]`                                                                                                                                                                                                    | undefined            |
| excludeFiat       | string[]?                                                                                                                                                         | `["USD"]`                                                                                                                                                                                                           | undefined            |
| onlyGateways      | string[]?                                                                                                                                                         | `["Wyre", "Moonpay"]`                                                                                                                                                                                               | undefined            |
| isAddressEditable | boolean?                                                                                                                                                          | `false`                                                                                                                                                                                                             | true                 |
| color             | string?                                                                                                                                                           | `"#000000"`                                                                                                                                                                                                         | "#31a5ff"            |
| fontFamily        | string?                                                                                                                                                           | `Arial, Helvetica, sans-serif`                                                                                                                                                                                      | 'Roboto', sans-serif |

## Javascript

###### Setup

Add an empty `div` tag to mark the spot where you want to display the widget and add a unique id to it.

```html
<div id="onramper-widget"></div>
```

Then, add three `script` tags to load the necessary dependencies (React, ReactDOM) and the widget:

```html
<!-- Load React. -->
<!-- Note: when deploying, replace "development.js" with "production.min.js". -->
<script
  src="https://unpkg.com/react@16/umd/react.development.js"
  crossorigin
></script>
<script
  src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"
  crossorigin
></script>

<!-- Load Onramper's widget. -->
<script src="https://unpkg.com/@onramper/widget/dist/index.js" crossorigin></script>
```

After the three scripts load, add the widget to the DOM invoking the `initialize` function

```javascript
Onramper.initialize("#onramper-widget");
```

###### Code snippet

```javascript
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Static website</title>
    <script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
    <script src="https://unpkg.com/@onramper/widget/index.js" crossorigin></script>
    <style>
      html,
      body {
        margin: 0;
        height: 100%;
      }
      #onramper-widget {
        width: 440px;
        height: 595px;
        box-shadow: 3px 3px 5px 0px rgba(0, 0, 0, 0.75);
        margin: 3rem auto;
      }
    </style>
  </head>
  <body>
    <div id="onramper-widget"></div>
    <script>
      Onramper.initialize("#onramper-widget");
    </script>
  </body>
</html>

```

###### Live example

<a href="https://codesandbox.io/s/onramper-widget-cdn-import-4zvfs" target='_blank' >CodeSandbox</a>

#### Initialize parameters

[For all parameters see CUSTOMIZE section](#customize)

| Name              | Type                                                                                                                                                              | Example                                                                                                                                                                                                                                                   | Default value |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| API_KEY           | string?                                                                                                                                                           | `Onramper.initialize("#id", {API_KEY:"YourAPIkey"})` <a href="https://docs.google.com/forms/d/e/1FAIpQLSdnmTskkGA5QJGjC1eVRcqXZouuGe_ojltlBFs5nFClrSl_gA/viewform?usp=sf_link" target='_blank' >(fill in our onboarding form to receive your API key)</a> | undefined     |
| defaultCrypto     | string?                                                                                                                                                           | `Onramper.initialize("#id", {defaultCrypto:"ETH"})`                                                                                                                                                                                                       | undefined     |
| defaultFiat       | string?                                                                                                                                                           | `Onramper.initialize("#id", {defaultFiat:"EUR"})`                                                                                                                                                                                                         | "USD"         |
| defaultAmount     | number?                                                                                                                                                           | `Onramper.initialize("#id", {defaultAmount:500"})`                                                                                                                                                                                                        | 100           |
| defaultAddrs      | object?                                                                                                                                                           | `Onramper.initialize("#id", {defaultAddrs:{"BTC": { address: "btcAddr" }}})`                                                                                                                                                                              | {}            |
| filters           | An object containing the attributes `onlyCryptos`, `excludeCryptos`, `onlyPaymentMethods`, `excludePaymentMethods`, `excludeFiat`, `onlyGateways` and `onlyFiat`. | `Onramper.initialize("#id", {filters:{onlyCryptos:["BTC", "ETH", "NEO"]}})`                                                                                                                                                                               | {}            |
| onlyCryptos       | string[]?                                                                                                                                                         | `Onramper.initialize("#id", {filters:{onlyCryptos:["BTC", "ETH", "NEO"]}})`                                                                                                                                                                               | undefined     |
| excludeCryptos    | string[]?                                                                                                                                                         | `Onramper.initialize("#id",{filters:{excludeCryptos:["ETH", "NEO"]}})`                                                                                                                                                                                    | undefined     |
| onlyFiat          | string[]?                                                                                                                                                         | `Onramper.initialize("#id",{filters:{onlyFiat:["EUR"]}})`                                                                                                                                                                                                 | undefined     |
| excludeFiat       | string[]?                                                                                                                                                         | `Onramper.initialize("#id", {filters:{excludeFiat:["EUR"]}})`                                                                                                                                                                                             | undefined     |
| onlyGateways      | string[]?                                                                                                                                                         | `Onramper.initialize("#id", {filters:{onlyGateways:["Moonpay"]}})`                                                                                                                                                                                        | undefined     |
| isAddressEditable | boolean?                                                                                                                                                          | `Onramper.initialize("#id", {isAddressEditable:false"})`                                                                                                                                                                                                  | true          |
| color             | string?                                                                                                                                                           | `Onramper.initialize("#id", {color:"#000000"})`                                                                                                                                                                                                           | "#31a5ff"     |
| fontFamily        | string?                                                                                                                                                           | `Onramper.initialize("#id", {fontFamily:"Arial, Helvetica, sans-serif"})`                                                                                                                                                                                 | "#31a5ff"     |

## Native apps

You can also include Onramper's widget in any native application using a WebView or any component that is able to render a website, as if it was an iframe, for this, you should point the source URI to `https://widget.onramper.com?apiKey=YOURAPIKEY`. You can also customize it using the [URL parameters](#url-parameters).

Don't forget that iframes and webviews are isolated components so you should enable some features in order to allow the widget to work properly.

This features are:

- Camera and storage permission (in order to upload KYC documents)
- Features: accelerometer; autoplay; camera; gyroscope; payment (required by one or more gateways in order to work properly)
- Allow third party cookies (used by one or more gateways)
- Allow the webview to open URLs automatically, without user interaction (payment redirects required by one or more gateways)
- Allow the webview to open URLs with the OS browser (payment redirects required by one or more gateways)

## Customize

You can pass the following arguments to customize the widget. In React/JS integrations the attributes `onlyCryptos`, `excludeCryptos`, `onlyPaymentMethods`, `excludePaymentMethods`, `excludeFiat`, `onlyGateways` and `onlyFiat` should be contained in an object under the attribute `filters`.

| Name                    | Description                                                                                                                                                                                         |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API_KEY                 | Production or test API Key.                                                                                                                                                                         |
| defaultCrypto           | Select a specific cryptocurrency by default. Should be specified the cryptocurrency code.                                                                                                           |
| defaultFiat             | Fiat currency to select by default.                                                                                                                                                                 |
| defaultFiatSoft         | Fiat currency to select by default only when the country currency is unavailable.                                                                                                                   |
| defaultPaymentMethod    | Payment method to select by default. [See posible values here.](#payment-method-ids)                                                                                                                |
| defaultAmount           | Positive integer representing the base amount of fiat to be filled in the widget. Should be indicated in USD, for other currencies, a rounded aproximated conversion will be automatically applied. |
| defaultAddrs \| wallets | Used to autofill the crypto address of the user.                                                                                                                                                    |
| onlyCryptos             | A comma-separated list of crypto codes to include. Only this cryptos will be shown to the user.                                                                                                     |
| filters                 | An object containing the attributes `onlyCryptos`, `excludeCryptos`, `onlyPaymentMethods`, `excludePaymentMethods`, `excludeFiat`, `onlyGateways` and `onlyFiat`. Only for React/JS integrations.   |
| excludeCryptos          | A comma-separated list of crypto codes to exclude. This cryptos will be excluded from the list of available cryptos.                                                                                |
| onlyFiat                | Only the fiat currencies added here will be available to pick.                                                                                                                                      |
| excludeFiat             | The fiat currencies added here will be excluded from the available ones.                                                                                                                            |
| onlyPaymentMethods      | Only the payment methods added here will be available to pick. [See posible values here.](#payment-method-ids)                                                                                      |
| excludePaymentMethods   | The payment methods added here will be excluded from the available ones. [See posible values here.](#payment-method-ids)                                                                            |
| onlyGateways            | Only the gateways added here will be availables. By default all are availables.                                                                                                                     |
| isAddressEditable       | Allow the user to edit the crypto address that is passed through the parameter defaultAddrs or wallets.                                                                                             |
| color                   | Color to change the highlight of the widget. Should be an hex color.                                                                                                                                |
| fontFamily              | Font to use in the widget.                                                                                                                                                                          |
| gFontPath               | Allows you to load a remote Google Font. Eg. `css2?family=Roboto:wght@400;500&display=swap` widget.                                                                                                 |
| redirectURL             | URL to redirect the user once a transaction is finished. Should be encoded.                                                                                                                         |

#### Payment method IDs

IDs of all posible payment methods:

`creditCard`, `bankTransfer`, `applePay`, `googlePay`, `paynow`, `fps`, `alipay-hk`, `prompt-pay`, `instapay`, `upi`, `gojek-id`, `viettel-pay`, `duit-now`
