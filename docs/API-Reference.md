## Countries
Country can be overwriten by providing it's ISO 3166 alpha-2 code (eg: 'us', 'gb'...). To get the a union of the available options for all countries just set the country to 'all'.

## gateways
Endpoint: `https://api.onramper.dev/gateways`  

##### Options
- **country**: `https://api.onramper.dev/gateways?country=es`
- **icons**: `https://api.onramper.dev/gateways?includeIcons=true`
- **cryptoCurrencies**: `https://api.onramper.dev/gateways?cryptoCurrencies=btc,neo`
- **fiatCurrencies**: `https://api.onramper.dev/gateways?fiatCurrencies=eu,usd`

Also provides localization data on the user, which can be used to customize the widget.

## rates
Endpoint: `https://api.onramper.dev/rate/{fromCurrency}/{toCurrency}/{paymentMethod}/{amount}`  
Example: `https://api.onramper.dev/rate/EUR/BTC/creditCard/100`

##### Options
  - **country**: `?country=es`
  - **icons**: `?includeIcons=true`
  - **amountInCrypto**: `?amountInCrypto=true`
