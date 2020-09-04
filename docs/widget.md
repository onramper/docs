# Widget

## Redirect / Iframe

#### URL Redirect
Redirect the user to our buy page.

###### HTML code snippet
```html
<a href="https://widget.onramper.dev?color=346eeb">
    Buy Crypto
</a>
```

###### Live example
<a href="https://widget.onramper.dev/" target='_blank' >Codepen</a>

#### Iframe
Embed an iframe in your website.

###### HTML code snippet
```html
<iframe
    src="https://widget.onramper.dev?color=346eeb"
    height="595px"
    width="440px"
    title="Onramper widget"
    frameborder="no"
    allowtransparency="true"
    style="box-shadow: 3px 3px 5px 0px rgba(0,0,0,0.75);">
</iframe>
```
###### Live example
<a href="https://widget.onramper.dev" target='_blank' >Codepen</a>

| Name           | Type         | Format                                    | Default value          |
|----------------|--------------|-------------------------------------------|------------------------|
| defaultCrypto  | Query string | `CRYPTO_CODE`                             | First available crypto |
| defaultAmount  | Query string | `100`                                     | 100                    |
| defaultAddrs   | Query string | `{"CRYPTO_CODE":["ADDR1", "ADDRN"], ...}` |                        |
| onlyCryptos    | Query string | `CRYPTO1_CODE,CRYPTO2_CODE2,...`          |                        |
| excludeCryptos | Query string | `CRYPTO1_CODE,CRYPTO2_CODE2,...`          |                        |
| color          | Query string | `HEX_COLOR`                               | 31a5ff                 |

## React component
###### Installation

```shell
# Using yarn
$ yarn add @onramper/widget

# Using npm
$ npm install @onramper/widget
```

###### Code snippet
```javascript
import OnramperWidget from '@onramper/widget'

<div style={{height:'595px', width:'440px'}}>
    <OnramperWidget color='346eeb' />
</div>
```
###### Live example
<a href="https://widget.onramper.dev/?apiKey=YOUR_API_KEY&color=000000" target='_blank' >Codepen</a>

#### Component parameters
| Name           | Type     | Format                                    | Default value          |
|----------------|----------|-------------------------------------------|------------------------|
| defaultCrypto  | String   | `"CRYPTO_CODE"`                           | First available crypto |
| defaultAmount  | Number   | `100`                                     | 100                    |
| defaultAddrs   | Object   | `{"CRYPTO_CODE":["ADDR1", "ADDRN"], ...}` |                        |
| onlyCryptos    | String[] | `["CRYPTO1_CODE","CRYPTO2_CODE2",...]`    |                        |
| excludeCryptos | String[] | `["CRYPTO1_CODE","CRYPTO2_CODE2",...]`    |                        |
| color          | String   | `"#HEX_COLOR"`                            | "#31a5ff"              |

## Parameters description
- **defaultCrypto:** Select a specific cryptocurrency by default. Should be specified the cryptocurrency code. `?defaultCrypto=ETH`
- **defaultAmount:** Fill a default amount of fiat. The amount should be in USD, then a conversion will be applied to the other currencies. `?defaultAmount=200`
- **addresses:** Available addresses that the user will be able to pick once he is asked for a wallet address to receive the funds. `?addresses={"BTC":["btcAddr1","btcAddr2"],"ETH":["ethAddr1"],"NEO":["neoAddr1","neoAddr2","neoAddr3","neoAddr4"]}`
- **onlyCryptos:** Filter. Specify which cryptos will be shown to the user. Should be specified the cryptocurrencies codes. `?onlyCryptos=ETH,BTC,NEO`
- **excludeCryptos:** Filter. Specify a list of cryptos that sholdn't be shown to the user. Should be specified the cryptocurrencies codes.. `?excludeCryptos=ETH,BTC,NEO`
- **color:** Highlight color in HEX `?color=346eeb`

<!-- If one of the cryptos is not available in the user's region, then the filter for this specific crypto is not applied -->