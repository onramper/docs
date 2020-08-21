# Widget

## Iframe / URL Redirect
Object parameters should be sent as an stringified JSON.  
Example`"{'BTC':['addr1','addr2']}"`

String[] parameters should be sent a list of items.  
Example `CRYPTO_CODE1,CRYPTO_CODE2,CRYPTO_CODE3`

#### URL Redirect
###### Code snippet
```html
<a href="https://widget.onramper.dev/?apiKey=YOUR_API_KEY">
    Buy Crypto
</a>
```

###### Live
<a href="https://widget.onramper.dev/?apiKey=YOUR_API_KEY" target='_blank' >Codepen</a>

#### Iframe
###### Code snippet
```html
<iframe
    height="595px"
    width="440px"
    title="Onramper widget"
    src="https://widget.onramper.dev/?apiKey=YOUR_API_KEY"
    frameborder="no"
    allowtransparency="true"
    style="box-shadow: 3px 3px 5px 0px rgba(0,0,0,0.75);">
</iframe>
```
###### Live
<a href="https://widget.onramper.dev" target='_blank' >Codepen</a>

## React
###### Code snippet

```shell
# Using yarn
$ yarn add @onramper/onramper-widget

# Using npm
$ npm install @onramper/onramper-widget
```

```javascript
import OnramperWidget from '@onramper/onramper-widget'

<div style="height:900px; width:600px;">
    <OnramperWidget apiKey='AAA-BBB-CCC' color='#000000' />
</div>
```
###### Live
<a href="https://widget.onramper.dev/?apiKey=YOUR_API_KEY&color=000000" target='_blank' >Codepen</a>

## Query parameters
| Name              | Description                                                                                  | Type     | Format                              | Default value          |
|-------------------|----------------------------------------------------------------------------------------------|----------|-------------------------------------|------------------------|
| apiKey (required) | Unique api key.                                                                              | String   | `'AAA-BBB-CCC'`                     |                        |
| defaultCrypto     | Default crypto to select. If that crypto is not available then will be selected the default. | String   | `'CRYPTO_CODE'`                     | First available crypto |
| defaultAmount     | Fill a default amount of fiat.                                                               | Number   | `100`                               | 100                    |
| defaultAddrs      | Available addresses that the user can optionally pick once he is asked for a wallet address. | Object   | `{CRYPTO_CODE:[ADDR1, ADDR2, ...]}` |                        |
| onlyCryptos       | List of available cryptos to show to the user                                                | String[] | `[CRYPTO_CODE1, CRYPTO_CODE2, ...]` |                        |
| excludeCryptos    | List of cryptos to hide to the user.                                                         | String[] | `[CRYPTO_CODE1, CRYPTO_CODE2, ...]` |                        |
| width             | Width of the widget in pixels.                                                               | Number   | `595`                               | 595                    |
| height            | Height of the widget in pixels.                                                              | Number   | `440`                               | 440                    |
| color             | Highlight color.                                                                             | String   | `000000`                            | 31a5ff                 |