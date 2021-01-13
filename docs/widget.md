# Widget

Here you will find instructions to add the Onramper widget in your website or application. With just a few lines of code, you can allow your users to purchase cryptocurrencies from your web or app.

You can integrate the widget in four different ways:  
· Redirect your users to the widget URL. [See more.](#redirect)  
· Use an iframe or a webview to embed the widget in your application. [See more.](#iframe)  
· Import a component in your React application. [See more.](#react-component)   
· Add it to your static webpage using a CDN import. [See more.](#javascript)   

## Redirect


Using a URL redirect, you can simply redirect your users to a buy page. The widget url is `https://widget.onramper.com`

###### HTML code snippet
```html
<a href="https://widget.onramper.dev?color=1d2d50" target="_blank">
    Buy cryptocurrencies
</a>
```

###### Live example & customization
Easily customize the buy-page by changing the URL with the [available URL parameters.](#url-parameters)

Redirect customization examples: <a href="https://codesandbox.io/s/onramper-widget-url-redirect-m8tdo" target='_blank' >CodeSandbox</a>

## Iframe
Embed an iframe in your website. This is the easiest way to add the widget on your own page.

###### HTML code snippet
```html
<iframe
    src="https://widget.onramper.dev?color=346eeb"
    height="595px"
    width="440px"
    title="Onramper widget"
    frameborder="no"
    style="box-shadow: 3px 3px 5px 0px rgba(0,0,0,0.75);">
</iframe>
```
###### Live example & customization
<a href="https://codepen.io/thijsmaaslaw/pen/eYzbgXM" target='_blank' >Iframe customization example</a>

#### URL parameters
You can pass some arguments as query parameters to the URL to customize the widget

| Name           | Format                               | Example                                                | Default value |
| -------------- | ------------------------------------ | ------------------------------------------------------ | ------------- |
| apiKey         | Alphanumeric string                  | `?apiKey=yourAPIkey` <a href="mailto:apikeys@onramper.com" target='_blank' >(contact us for keys)</a>             | Not set       |
| defaultCrypto  | Cryptocurrency code                  | `?defaultCrypto=BTC`                                   | Not set       |
| defaultAmount  | Positive integer                     | `?defaultAmount=500`                                   | 100           |
| addresses   | Stringified JSON                     | `?addresses={"BTC":["addr1"],"ETH":["add1r","addr2"]}` | {}            |
| onlyCryptos    | Comma-separated list of crypto codes | `?onlyCryptos=BTC,ETH,NEO`                             | Not set       |
| excludeCryptos | Comma-separated list of crypto codes | `?excludeCryptos=BTC,ETH,NEO`                          | Not set       |
| color          | Hexadecimal color                    | `?color=346eeb`                                        | 31a5ff        |

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
| Name           | Type      | Example                              | Default value |
| -------------- | --------- | ------------------------------------ | ------------- |
| apiKey         | String?   | `"yourAPIkey"` <a href="mailto:apikeys@onramper.com" target='_blank' >(contact us for keys)</a>                       | undefined     |
| defaultCrypto  | String?   | `"ETH"`                              | undefined     |
| defaultAmount  | Number?   | `500`                                | 100           |
| defaultAddrs   | Object?   | `{"BTC":["ADDR1"], "ETH":["ADDR2"]}` | {}            |
| onlyCryptos    | String[]? | `["BTC", "ETH", "NEO"]`              | undefined     |
| excludeCryptos | String[]? | `["ETH", "NEO"]`                     | undefined     |
| color          | String?   | `"#000000"`                          | "#31a5ff"     |

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
<script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>

<!-- Load Onramper's widget. -->
<script src="https://unpkg.com/@onramper/widget/index.js" crossorigin></script>
```

After the three scripts load, add the widget to the DOM invoking the `initialize` function

```javascript
Onramper.initialize("#onramper-widget")
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
| Name           | Type      | Example                                                                         | Default value |
| -------------- | --------- | ------------------------------------------------------------------------------- | ------------- |
| apiKey         | String?   | `Onramper.initialize("#id", {apiKey:"YourAPIkey"})` <a href="mailto:apikeys@onramper.com" target='_blank' >(contact us for keys)</a>                             | undefined     |
| defaultCrypto  | String?   | `Onramper.initialize("#id", {defaultCrypto:"ETH"})`                             | undefined     |
| defaultAmount  | Number?   | `Onramper.initialize("#id", {defaultAmount:500"})`                              | 100           |
| defaultAddrs   | Object?   | `Onramper.initialize("#id", {defaultAddrs:{"BTC":["ADDR1"], "ETH":["ADDR2"]}})` | {}            |
| onlyCryptos    | String[]? | `Onramper.initialize("#id", {onlyCryptos:["BTC", "ETH", "NEO"]})`               | undefined     |
| excludeCryptos | String[]? | `Onramper.initialize("#id", {excludeCryptos:["ETH", "NEO"]})`                   | undefined     |
| color          | String?   | `Onramper.initialize("#id", {color:"#000000"})`                                 | "#31a5ff"     |



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
