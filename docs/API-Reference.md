## API overview

##### Authentication

With any request, you should include the header `Authorization` with value `Basic API_KEY`. For example `Basic pk_prod_xxxxxxxxxxxxxxxxxxxxxxxx`.

Example cURL command with Basic Authorization header for the Gateways endpoint:
```
curl --location --request GET 'https://onramper.tech/gateways' \
--header 'Authorization: Basic pk_prod_xxxxxxxxxxxxxxxxxxxxxxxx'
```

## Gateways

Endpoint: `GET https://onramper.tech/gateways`

Get a list of available gateways. The info provided about these gateways is: the cryptocurrencies, currencies an payment methods accepted. It also provides localization data on the user, which can be used to customize the widget. [See response type definitions here](https://github.com/onramper/widget/tree/master/package/src/ApiContext/api/types).

##### Options

| Option       | Description                                                                                                                                                                                                                                                                                                                                   |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| country      | Defines which gateways are available. By default, the country is automatically detected by the API using client's IP but it can be overwriten by providing it's ISO 3166 alpha-2 code (eg: 'us', 'gb'...). To get all the available options for all countries just set the country to 'all'. `E.g. https://onramper.tech/gateways?country=es` |
| includeIcons | If `true`, includes icons of the cryptos, currencies and payment methods in the response. `E.g. https://onramper.tech/gateways?includeIcons=true`                                                                                                                                                                                             |

##### Example response

`https://onramper.tech/gateways`

```json
{
  "gateways": [
    {
      "identifier": "Wyre",
      "paymentMethods": ["creditCard", "bankTransfer"],
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
    }
  ],
  "localization": {
    "country": "es",
    "state": null,
    "currency": "EUR"
  }
}
```

## Rates

Endpoint: `GET https://onramper.tech/rate/{fromCurrency}/{toCurrency}/{paymentMethod}/{amount}`

Get a list of accessable gateways. Those gateways can be available or unavailable. The available gateways will have the attribute `available` set to `true`, and an [attribute `nextStep`](#steps) describing the first action to be done to start the [purchase flow](#purchase-flow). The unavailable gateways will have the attribute `available` set to `false`, and an attribute `error` describing why the gateway is unavailable (e.g. Maximum amount exceeded).

Url variables `{fromCurrency}` and `{toCurrency}` should be filled with currency codes and `{paymentMethod}` should be filled with one of the payment methods id's. Codes and id's are availables on the attributes `cryptoCurrencies`, `fiatCurrencies` and `paymentMethods` from [`/gateways` response](#gateways). Url variable {amount} is a positive integer.

##### URL

- **fromCurrency**: The Currency to pay with. Currently, only fiat currencies are allowed.
- **toCurrency**: The Currency to buy. Currently, only cryptocurrencies are allowed.
- **paymentMethod**: The Payment method to use.
- **amount**: The amount of currency to buy, by default, amount of `fromCurrency`.

##### Options

| Option         | Description                                                                                                                                                                                                                                                                                                                            |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| country        | Defines which gateways are available. By default, country is automatically detected by the API using client's IP but can be overwriten by providing it's ISO 3166 alpha-2 code (eg: 'us', 'gb'...). To get all the available options for all countries just set the country to 'all'. `E.g. https://onramper.tech/gateways?country=es` |
| includeIcons   | If `true`, includes icons of the cryptos, currencies and payment methods in the response. `E.g. https://onramper.tech/gateways?includeIcons=true`                                                                                                                                                                                      |
| amountInCrypto | If `true`, the amount specified in `{amount}` represents the amount of crypto user wants to buy. `E.g. https://onramper.tech/rate/EUR/BTC/creditCard/100?amountInCrypto=true`                                                                                                                                                          |

##### Example response

`https://onramper.tech/rate/EUR/BTC/creditCard/100`

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
      ["passport", "driverLicense", "nationalIdentityCard", "residenceCard"],
      "selfie"
    ],
    "receivedCrypto": 0.01013,
    "nextStep": {
      "type": "form",
      "url": "https://onramper.tech/transaction/Moonpay/email/WyJ0VjVIQWpaQ3lsUzZVRHJxRDhqN0FBLS0iLDEwMCwiRVVSIiwiQlRDIiwiY3JlZGl0Q2FyZCJd",
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

The purchase flow is split in different steps, and depends on the gateway used for the transaction. Users should complete all steps to make a successful purchase.

##### First step

You will find the first step to execute in the attribute `nextStep` of the available gateway selected from the `/rate` response and the following steps as the response of the executed step.

If you want to attach a custom object to the transaction started by users, then you should append it to the body of the `POST` request of the first step (usually a `form` a `wait` step). You should add your custom object under the key `partnerContext` in the request body. In case the first step is a `form` step, the `partnerContext` key will be next to the other requested fields.

##### Purchase flow

1. First we call to `/gateways` to get a list of the cryptos, currencies and payment methods availables.
2. Once we have selected the `fromCurrency`, the `toCurrency`, the `paymentMethod` and the `amount` we want to buy, we make a call to `/rates` to know which gateways are availables for that combination.
3. If the amount is enough to give us at least one gateway available, we can start the process of buying crypto. If not, we should make another call fixing one of the errors described in the attribute `error`.
4. Now that we have selected the gateway we want to use, we should check the attribute `nextStep` to know which is the first step to start with the purchase flow.
5. Here you have a ([list of posible steps](#steps)) and instructions to how to execute them.
6. Once we complete a step, we will get a new step on the response. We will keep executing steps until the flow is finished.

![title](images/flow.png)

##### Step types

[Steps implementation example](https://github.com/onramper/widget/tree/master/package/src/steps)

| Step                   | Description                                                                                                                                                                                                                                                                                                                                                                  |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| wait                   | Waiting step. The server is processing some data and there's no action to be done now, user should wait. To execute make a `POST` request to the `url` attribute. The response will be another waiting step until the server has finished the current data processing, the app should query the following waiting steps until the server responds with another type of step. |
| form                   | Form step. Describes a set of fields that should be filled by the user. To execute, make a `POST` request to the `url` attribute with the fields as a body request.                                                                                                                                                                                                          |
| iframe                 | External widget/iframe step, required in the flow of some gateways (for payment/KYC). To execute this step, display to the user an iframe of the `url` attribute, listen to 'messages' of the iframe window to get the next step.                                                                                                                                            |
| redirect               | The user should be redirected to the url specified in the `url` attribute. Listen to 'messages' of the redirected window to get the next step.                                                                                                                                                                                                                               |
| pickOne                | User can choose to complete one of the steps listed in the `options` attribute.                                                                                                                                                                                                                                                                                              |
| file                   | User should upload a file. To execute make a `PUT` request to the `url` attribute.                                                                                                                                                                                                                                                                                           |
| completed              | The purrchase flow is completed. No more steps needed.                                                                                                                                                                                                                                                                                                                       |
| requestBankTransaction | The purrchase flow is completed. User should complete a bank payment.                                                                                                                                                                                                                                                                                                        |

##### Example response

Given

```json
....
"nextStep": {
      "type": "form",
      "url": "https://onramper.tech/transaction/Moonpay/email/WyJ0VjVIQWpaQ3lsUzZVRHJxRDhqN0FBLS0iLDEwMCwiRVVSIiwiQlRDIiwiY3JlZGl0Q2FyZCJd",
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
  "cryptocurrencyAddress": "0xce46a79f871cf0b05a5ef20ff041c92a007d507e",
  // only if it's the first step and you want to attach a custom context
  "partnerContext": {
    myTxId: "TwQC716Q8D",
    myUserId: 65165468,
    lastTab: "wallet-funds",
  }
}
```

If the body is correct, we will get a new step in the response, if not, we will get an error, for example:

```json
{
  "message": "The provided cryptocurrency address is not valid.",
  "field": "cryptocurrencyAddress"
}
```

Success step response example (the response is a new step):

```json
{
  "type": "form",
  "url": "https://onramper.tech/transaction/Moonpay/verifyEmail/WyJIQVdMOGJwM1I4RmFMeGpDTUNTOUtnLS0iLCJkYXJlbjQ0dl93NDgxbEB4ZWRtaS5jb20iXQ==",
  "data": [
    {
      "type": "string",
      "name": "verifyEmailCode",
      "humanName": "Email verification code"
    }
  ]
}
```

## Testing

To execute the transactions in a testing enviroment make sure you use your test API Key in the `Authorization` header. For example `Basic pk_test_xxxxxxxxxxxxxxxxxxxxxxxx`.
When testing a transaction to buy BTC, make sure to use a test-net wallet address. An example testnet address you could use is: 2N3oefVeg6stiTb5Kh3ozCSkaqmx91FDbsm

**Moonpay**

Test card number for 3D Secure transactions
Visa `4000 0209 5159 5032` `12/2022` `123`

Test card number for declined transactions
Visa `4000 3198 7280 7223` `12/2022` `123`

**Wyre**

Test card number
`4111 1111 1111 1111` `01/2023` `123`

2FA codes (sms/card)
`000000`

**Indacoin**

_Valid for only `INTT` `(Indacoin Test Tokens)` transactions._

Test card number

`4111 1111 1111 1111`  `03/2023`  `123`

## Webhooks

Webhooks perform signed POST requests about specific events to a URL of your choice. If you respond with a 2xx code, our system will consider the webhook as successfully sent and received.

In order to receive webhooks, you must provide Onramper with a URL that the webhooks will be sent to. A shared secret will be shared privately with you in order to verify the webhook payload's signature. Contact us for this secret.

**Payload**

| Key                        | Description                                                                         |
| -------------------------- | ----------------------------------------------------------------------------------- |
| txId `string`              | Unique transaction identifier.                                                      |
| inAmount `number`          | A positive integer representing how much the user is charged.                       |
| inCurrency `string`        | The identifier of the fiat currency the user wants to use for the transaction.      |
| outAmount `number`         | A positive integer representing the amount of cryptocurrency the user will receive. |
| outCurrency `string`       | The identifier of the cryptocurrency the user wants to purchase.                    |
| timestamp `number`         | Time at which the object was created. Returned as Unix timestamp.                   |
| gatewayIdentifier `string` | The identifier of the gateway used to execute the purchase.                         |
| medium `string`            | Payment method the user used (currently disabled)                                   |
| partnerContext `object`    | Context for this event. Free context for partners to receive in webhooks.           |

Example:

```json
{
  "txId": "f5377a92-0fb5-4bc2-a759-b554ad4fb769",
  "inAmount": 204.45,
  "inCurrency": "USD",
  "outAmount": 0.0036,
  "outCurrency": "BTC",
  "timestamp": 1619946830511,
  "gatewayIdentifier": "Moonpay",
  "medium": "undefined",
  "partnerContext": {
    "myTxId": "TwQC716Q8D",
    "myUserId": 65165468,
    "lastTab": "wallet-funds"
  }
}
```

#### Partner context

If you would like to receive a custom data set by you in the webhook payload you should send it in the body of the `POST` request of the [first step]('#first-step') of the purchase process. The first step of any purchase process is the step defined in the `nextStep` attribute of the `/rate` response. Currently is functionality is only available for `Moonpay` and `Wyre`.

#### Securing Webhooks

To ensure the integrity of the data contained in the webhook, Onramper signs all webhooks sent with a shared secret that is known only by you and Onramper.

Signing the webhooks is done using `HMAC-SHA256` with the shared secret as the key and the full request body as the message. The resulting signature is provided in the `X-Onramper-Webhook-Signature` HTTP header.

In order to verify the webhook signature, compute a HMAC with the SHA-256 hash function. Use the shared secret as the key, and use the full request body string as the message in both cases. Then compare the signature in the header with the expected signature.

## Available gateways

#### Wyre

- Available in production.
- Partner context available.
- Onramper's custom flow.

#### Moonpay

- Available in production.
- Partner context available.
- Moonpay's widget flow available through the API.
- Onramper's custom flow available through an adapter. In order to use the custom Onramper flow with Moonpay you should use the [npm package `@onramper/moonpay-adapter`](https://www.npmjs.com/package/@onramper/moonpay-adapter), it works like a fetch mock so when Moonpay is selected, you will just have to forward the request to the Moonpay adapter. This is because of Moonpay policies, the code should be executed client side.

#### Xanpool

- Available in production.
- Xanpool's widget flow.
- Partner context soon will be supported.

#### Mercuryo

- Available in production.
- Mercuryo's widget flow.
- Partner context soon will be supported.

#### Coinify

- Available only for test enviroment. Soon in production.

#### Indacoin

- Avaliable only for test environment. Soon in production.
