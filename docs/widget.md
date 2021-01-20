# Widget

Here you will find instructions to add the Onramper widget in your website or application. With just a few lines of code, you can allow your users to purchase cryptocurrencies from your web or app.

You can integrate the widget in four different ways:  
· Redirect your users to the widget URL. [See more.](#redirect)  
· Use an iframe or a webview to embed the widget in your application. [See more.](#iframe)  
· Import a component in your React application. [See more.](#react-component)  
· Add it to your static webpage using a CDN import. [See more.](#javascript)

# API Key
To allow users to buy crypto, you need an API key. To get an API key, fill in <a href="https://docs.google.com/forms/d/e/1FAIpQLSdnmTskkGA5QJGjC1eVRcqXZouuGe_ojltlBFs5nFClrSl_gA/viewform?usp=sf_link" target='_blank' >our onboarding form.</a>
Add your API key as a parameter in the URL of the code snippet as follows: `https://widget.onramper.com?apiKEY=theAPIkeyyoureceived`. 

## Redirect

Using a URL redirect, you can simply redirect your users to a buy page. The widget url is `https://widget.onramper.com`

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

Note: In order to enable the widget for transactions, don't forget to [add the API key](#API-key). In order to enable some features in the widget, don't forget to add the allow attribute to the iframe element. 

###### HTML code snippet

```html
<iframe
  src="https://widget.onramper.com?color=346eeb"
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

| Name              | Format                                            | Example                                                                                               | Default value |
| ----------------- | ------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ------------- |
| apiKey            | Alphanumeric string                               | `?apiKey=yourAPIkey` <a href="https://docs.google.com/forms/d/e/1FAIpQLSdnmTskkGA5QJGjC1eVRcqXZouuGe_ojltlBFs5nFClrSl_gA/viewform?usp=sf_link" target='_blank' >(fill in our onboarding form to receive your API key)</a> | Not set       |
| defaultCrypto     | Cryptocurrency code                               | `?defaultCrypto=BTC`                                                                                  | BTC           |
| defaultFiat       | Fiat code                                         | `?defaultFiat=EUR`                                                                                    | USD           |
| defaultAmount     | Positive integer                                  | `?defaultAmount=500`                                                                                  | 100           |
| wallets           | Comma-separated list of crypto code:address pairs | `?wallets=BTC:btcaddr,ETH:erc20addr`                                                                  | Not set       |
| onlyCryptos       | Comma-separated list of crypto codes              | `?onlyCryptos=BTC,ETH,NEO`                                                                            | Not set       |
| excludeCryptos    | Comma-separated list of crypto codes              | `?excludeCryptos=BTC,ETH,NEO`                                                                         | Not set       |
| excludeFiat       | Comma-separated list of fiat codes                | `?excludeCryptos=EUR,USD`                                                                             | Not set       |
| onlyFiat          | Comma-separated list of fiat codes                | `?onlyFiat=EUR,USD`                                                                                   | Not set       |
| onlyGateways      | Comma-separated list of gateway identifiers       | `?onlyGateways=Wyre,Moonpay`                                                                          | Not set       |
| isAddressEditable | Boolean value                                     | `?isAddressEditable=false`                                                                            | true          |
| color             | Hexadecimal color                                 | `?color=346eeb`                                                                                       | 31a5ff        |

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

const userAddresses = {
    "BTC": ["addr1"],
    "ETH": ["add1r","addr2"]
}

export default function WidgetContainer() {
  return (
    <div
      style={{
        width: "440px",
        height: "595px"
      }}
    >
      <OnramperWidget defaultCrypto="BTC" />
    </div>
  )


  <OnramperWidget defaultAddrs={userAddresses} />;
}
```

###### Live example & customization

While importing the widget as a React component, you can customize it using the component props below.
<a href="https://codesandbox.io/s/onramper-widget-react-component-y3nd1" target='_blank' >CodeSandbox</a>

#### Component props

| Name              | Type      | Example                                                                                         | Default value |
| ----------------- | --------- | ----------------------------------------------------------------------------------------------- | ------------- |
| API_KEY           | string?   | `"yourAPIkey"` <a href="mailto:apikeys@onramper.com" target='_blank' >(contact us for keys)</a> | undefined     |
| defaultCrypto     | string?   | `"ETH"`                                                                                         | undefined     |
| defaultFiat       | string?   | `"EUR"`                                                                                         | "USD"         |
| defaultAmount     | number?   | `500`                                                                                           | 100           |
| defaultAddrs      | object?   | `{"BTC":["ADDR1"], "ETH":["ADDR2"]}`                                                            | {}            |
| onlyCryptos       | string[]? | `["BTC", "ETH", "NEO"]`                                                                         | undefined     |
| excludeCryptos    | string[]? | `["ETH", "NEO"]`                                                                                | undefined     |
| onlyFiat          | string[]? | `["USD", "EUR"]`                                                                                | undefined     |
| excludeFiat       | string[]? | `["USD"]`                                                                                       | undefined     |
| onlyGateways      | string[]? | `["Wyre", "Moonpay"]`                                                                           | undefined     |
| isAddressEditable | boolean?  | `false`                                                                                         | true          |
| color             | string?   | `"#000000"`                                                                                     | "#31a5ff"     |

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
<script src="https://unpkg.com/@onramper/widget/index.js" crossorigin></script>
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

| Name              | Type      | Example                                                                                                                               | Default value |
| ----------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| API_KEY           | string?   | `Onramper.initialize("#id", {API_KEY:"YourAPIkey"})` <a href="mailto:apikeys@onramper.com" target='_blank' >(contact us for keys)</a> | undefined     |
| defaultCrypto     | string?   | `Onramper.initialize("#id", {defaultCrypto:"ETH"})`                                                                                   | undefined     |
| defaultFiat       | string?   | `Onramper.initialize("#id", {defaultFiat:"EUR"})`                                                                                     | "USD"         |
| defaultAmount     | number?   | `Onramper.initialize("#id", {defaultAmount:500"})`                                                                                    | 100           |
| defaultAddrs      | object?   | `Onramper.initialize("#id", {defaultAddrs:{"BTC":["ADDR1"], "ETH":["ADDR2"]}})`                                                       | {}            |
| onlyCryptos       | string[]? | `Onramper.initialize("#id", {onlyCryptos:["BTC", "ETH", "NEO"]})`                                                                     | undefined     |
| excludeCryptos    | string[]? | `Onramper.initialize("#id", {excludeCryptos:["ETH", "NEO"]})`                                                                         | undefined     |
| onlyFiat          | string[]? | `Onramper.initialize("#id", {onlyFiat:["EUR"]})`                                                                                      | undefined     |
| excludeFiat       | string[]? | `Onramper.initialize("#id", {excludeFiat:["EUR"]})`                                                                                   | undefined     |
| onlyGateways      | string[]? | `Onramper.initialize("#id", {onlyGateways:["Moonpay"]})`                                                                              | undefined     |
| isAddressEditable | boolean?  | `Onramper.initialize("#id", {isAddressEditable:false"})`                                                                              | true          |
| color             | string?   | `Onramper.initialize("#id", {color:"#000000"})`                                                                                       | "#31a5ff"     |

## Customize

You can pass the following arguments to customize the widget

| Parameter      | Description                                                                                                                                                                                                                        |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| defaultCrypto  | Select a specific cryptocurrency by default. Should be specified the cryptocurrency code.                                                                                                                                          |
| defaultAmount  | Positive integer representing the base amount of fiat to be filled in the widget. Should be indicated in USD, for other currencies, a rounded aproximated conversion will be automatically applied.                                |
| addresses      | A stringified JSON with the wallet addresses of the user. The keys should be the cryptocurrency code and the value a list containing the user addresses. Can be more than one address per wallet and more than one cryptocurrency. |
| onlyCryptos    | A comma-separated list of crypto codes to include. Only this cryptos will be shown to the user.                                                                                                                                    |
| excludeCryptos | A comma-separated list of crypto codes to exclude. This cryptos will be excluded from the list of available cryptos..                                                                                                              |
| color          | Color to change the highlight of the widget. Should be an hex color.                                                                                                                                                               |

| Name                    | Description                                                                                                                                                                                                                        |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API_KEY                 | Production or test API Key.                                                                                                                                                                                                        |
| defaultCrypto           | Select a specific cryptocurrency by default. Should be specified the cryptocurrency code.                                                                                                                                          |
| defaultFiat             | Fiat currency to select by default when the country currency is unavailable.                                                                                                                                                       |
| defaultAmount           | Positive integer representing the base amount of fiat to be filled in the widget. Should be indicated in USD, for other currencies, a rounded aproximated conversion will be automatically applied.                                |
| defaultAddrs \| wallets | A stringified JSON with the wallet addresses of the user. The keys should be the cryptocurrency code and the value a list containing the user addresses. Can be more than one address per wallet and more than one cryptocurrency. |
| onlyCryptos             | A comma-separated list of crypto codes to include. Only this cryptos will be shown to the user.                                                                                                                                    |
| excludeCryptos          | A comma-separated list of crypto codes to exclude. This cryptos will be excluded from the list of available cryptos.                                                                                                               |
| onlyFiat                | Only the fiat currencies added there will be available to pick.                                                                                                                                                                    |
| excludeFiat             | The fiat currencies added there will be excluded from the available ones.                                                                                                                                                          |
| onlyGateways            | Only the gateways added here will be availables. By default all are availables.                                                                                                                                                    |
| isAddressEditable       | Allow the user to edit the crypto address that is passed through the parameter defaultAddrs or wallets.                                                                                                                            |
| color                   | Color to change the highlight of the widget. Should be an hex color.                                                                                                                                                               |
