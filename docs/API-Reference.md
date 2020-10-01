## Gateways
Endpoint: `https://api.onramper.dev/gateways`  

Get a list of available gateways. The info provided of this gateways is the cryptocurrencies, currencies an payment methods accepted. Also provides localization data on the user, which can be used to customize the widget. [See response type definitions here](https://github.com/onramper/widget/tree/dev/src/OnramperWidget/ApiContext/api/types).

##### Options
| Option       | Description                                                                                                                                                                                                                                                                                                                                  |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| country      | Defines which gateways are available. By default is automatically detected by the API using client's IP but can be overwriten by providing it's ISO 3166 alpha-2 code (eg: 'us', 'gb'...). To get the a union of the available options for all countries just set the country to 'all'.  `E.g. https://api.onramper.dev/gateways?country=es` |
| includeIcons | If `true`, includes icons of the cryptos, currencies and payment methods in the response. `E.g. https://api.onramper.dev/gateways?includeIcons=true`                                                                                                                                                                                         |

##### Example response
`https://api.onramper.dev/gateways`
```json
{
  "gateways": [
    {
      "paymentMethods": [
        "creditCard",
        "bankTransfer"
      ],
      "fiatCurrencies": [
        {
          "code": "EUR",
          "precision": 2
        }
      ],
      "cryptoCurrencies": [
        {
          "code": "BTC",
          "precision": 5
        },
        {
          "code": "ETH",
          "precision": 5
        }
      ]
    },
  ],
  "localization": {
    "country": "es",
    "state": null,
    "currency": "EUR"
  }
}
```

## Rates
Endpoint: `https://api.onramper.dev/rate/{fromCurrency}/{toCurrency}/{paymentMethod}/{amount}`  

Get a list of accessable gateways. Those gateways can be availables or unavailables. The available gateways will have the attribute `available` set to `true`, and an [attribute `nextStep`](#steps) describing the first action should be done to start the [purchase flow](#purchase-flow). The unavailable gateways will have the attribute `available` set to `false`, and an attribute `error` describing why is the gateway unavailable (e.g. Maximum amount exceeded).

Url variables `{fromCurrency}` and `{toCurrency}` should be filled with currency codes and `{paymentMethod}` should be filled with one of the payment methods id's. Codes and id's are availables on the attributes `cryptoCurrencies`, `fiatCurrencies` and `paymentMethods` from [`/gateways` response](#gateways). Url variable {amount} is a positive integer.

##### URL
  - **fromCurrency**: Currency we want to pay with, currently only fiat currencies are allowed.
  - **toCurrency**: Currency we want to buy, currently only crypto currencies are allowed.
  - **paymentMethod**: Payment method we want to use.
  - **amount**: Amount of currency we want to buy, by default, amount of `fromCurrency`.

##### Options
| Option         | Description                                                                                                                                                                                                                                                                                                                                  |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| country        | Defines which gateways are available. By default is automatically detected by the API using client's IP but can be overwriten by providing it's ISO 3166 alpha-2 code (eg: 'us', 'gb'...). To get the a union of the available options for all countries just set the country to 'all'.  `E.g. https://api.onramper.dev/gateways?country=es` |
| includeIcons   | If `true`, includes icons of the cryptos, currencies and payment methods in the response. `E.g. https://api.onramper.dev/gateways?includeIcons=true`                                                                                                                                                                                         |
| amountInCrypto | If `true`, the amount specified in `{amount}` represents the amount of crypto user wants to buy. `E.g. https://api.onramper.dev/rate/EUR/BTC/creditCard/100?amountInCrypto=true`                                                                                                                                                             |

##### Example response
`https://api.onramper.dev/rate/EUR/BTC/creditCard/100`
```json
[
  {
    "identifier": "Moonpay",
    "duration": {
      "seconds": 600,
      "message": "~10 minutes"
    },
    "rate": 9377.48125,
    "available": true,
    "fees": 4.99,
    "requiredKYC": [
      "email",
      "identity",
      [
      "passport",
      "driverLicense",
      "nationalIdentityCard",
      "residenceCard"
      ],
      "selfie"
    ],
    "receivedCrypto": 0.01013,
    "nextStep": {
      "type": "form",
      "url": "https://api.onramper.dev/transaction/Moonpay/email/WyJ0VjVIQWpaQ3lsUzZVRHJxRDhqN0FBLS0iLDEwMCwiRVVSIiwiQlRDIiwiY3JlZGl0Q2FyZCJd",
      "data": [
        {
          "type": "string",
          "name": "email",
          "humanName": "Email",
          "hint": "We will send a code to your email."
        },
        {
          "type": "string",
          "name": "cryptocurrencyAddress",
          "humanName": "Cryptocurrency wallet address"
        }
      ]
    }
  },
  {
    "identifier": "CryptoCoin.pro",
    "duration": {
      "seconds": 50400,
      "message": "~14 hours"
    },
    "available": false,
    "error": {
      "type": "MIN",
      "message": "The minimum transaction accepted is 150 EUR",
      "limit": 150
    }
  }
]
```

## Steps
The purchase flow is splitted in different steps. User should complete all steps to make a successful purchase. You will find the first step to execute in the attribute `nextStep` of the available gateway selected from the `/rate` response and the following steps in the responses of the steps executed.

##### Purchase flow
1. First we call to `/gateways` to get a list of the cryptos, currencies and payment methods availables.
2. Once we have selected the `fromCurrency`, the `toCurrency`, the `paymentMethod` and the `amount` we want to buy, we make a call to `/rates` to know which gateways are availables for that combination.
3. If the amount is enough to give us at least one gateway available, we can start the process of buying crypto. If not, we should make another call fixing one of the errors described in the attribute `error`.
4. Now that we have selected the gateway we want to use, we should check the attribute `nextStep` to know which is the first step to start with the purchase flow.
5. Here you have a ([list of posible steps](#steps)) and instructions to how to execute them.
6. Once we complete a step, we will get a new step on the response. We will keep executing steps until the flow is finished.

![title](images/flow.png)

##### Step types
[Steps implementation example](https://github.com/onramper/widget/tree/dev/src/OnramperWidget/steps)

| Step                   | Description                                                                                                                                                        |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| form                   | Form step. Describes a set of fields that should be filled by the user. To execute make a `POST` request to the `url` attribute with the fields as a body request. |
| iframe                 | For execute this step, display to the user an iframe if the `url` attribute, listen to 'messages' of the iframe window to get the next step.                       |
| redirect               | The user should be redirected to the url specified in the `url` attribute. Listen to 'messages' of the redirected window to get the next step.                     |
| pickOne                | User can choose to complete one of the steps listed in the `options` attribute.                                                                                    |
| file                   | User should upload a file. To execute make a `PUT` request to the `url` attribute.                                                                                 |
| completed              | The purrchase flow is completed. No more steps needed.                                                                                                             |
| requestBankTransaction | The purrchase flow is completed. User should complete a bank payment.                                                                                              |


##### Example response

Given
```json
....
"nextStep": {
      "type": "form",
      "url": "https://api.onramper.dev/transaction/Moonpay/email/WyJ0VjVIQWpaQ3lsUzZVRHJxRDhqN0FBLS0iLDEwMCwiRVVSIiwiQlRDIiwiY3JlZGl0Q2FyZCJd",
      "data": [
        {
          "type": "string",
          "name": "email",
          "humanName": "Email",
          "hint": "We will send a code to your email."
        },
        {
          "type": "string",
          "name": "cryptocurrencyAddress",
          "humanName": "Cryptocurrency wallet address"
        }
      ]
    }
...
```

We make a request to `nextStep.url` with the following body:
```
{
  "email": "hello@onramper.com",
  "cryptocurrencyAddress": "0xce46a79f871cf0b05a5ef20ff041c92a007d507e"
}
```

If the body is correct, we will get a new step in the response, if not, we will get an error (e.g `{"message":"The provided cryptocurrency address is not valid.","field":"cryptocurrencyAddress"}`)

Success step response example (the response is a new step):

```json
{
   "type":"form",
   "url":"https://api.onramper.dev/transaction/Moonpay/verifyEmail/WyJIQVdMOGJwM1I4RmFMeGpDTUNTOUtnLS0iLCJkYXJlbjQ0dl93NDgxbEB4ZWRtaS5jb20iXQ==",
   "data":[
      {
         "type":"string",
         "name":"verifyEmailCode",
         "humanName":"Email verification code"
      }
   ]
}
```
