## gateways
Endpoint: `https://api.onramper.dev/gateways`
Options:
  - **country**: `https://api.onramper.dev/gateways?country=es`
  - **icons**: `https://api.onramper.dev/gateways?includeIcons=true`
  - **cryptocurrencies**: `https://api.onramper.dev/gateways?cryptocurrencies=btc,neo`
  - **currencies**: `https://api.onramper.dev/gateways?currencies=eu,usd`
Also provides localization data on the user, which can be used to customize the widget.

## rates
Endpoint: `https://api.onramper.dev/rate/{fromCurrency}/{toCurrency}/{paymentMethod}/{amount}`
Example: `https://api.onramper.dev/rate/EUR/BTC/creditCard/100`
Options:
  - **country**: `?country=es`
  - **icons**: `?includeIcons=true`
