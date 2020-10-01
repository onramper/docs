# API wrappers

## APIContext (React +  JS/TS)

```shell
# Using yarn
$ yarn add @onramper/onramper-context

# Using npm
$ npm install @onramper/onramper-context
```

```javascript
import { APIProvider } from '@onramper/onramper-context'

<APIProvider>
    <YourApp />
</APIProvider>
```

```javascript
import React, {useContext} from 'react'
import { APIContext } from '@onramper/onramper-context'

function YourApp() {
    const { data } = useContext(APIContext);

    return (
        <ul>
            {data.availableCryptos.map((crypto, i)=>{
                return <li key={i}>{crypto.code}</li>
            })}
        </ul>
    )
}
```

#### API Interface
`apiInterface.init(country?: string)`  
`apiInterface.executeStep(step: NextStep, params: { [key: string]: any })`  
`apiInterface.getRates()`

#### Data Interface
`data.handleCryptoChange(crypto?: ItemType)`  
`data.handleCurrencyChange(currency?: ItemType)`  
`data.handlePaymentMethodChange(paymentMethod?: ItemType)`

#### Input Interface
`inputInterface.handleInputChange(name: string, value: any)`

#### Collected Interface
`collected.amount`  
`collected.selectedCrypto`  
`collected.selectedCurrency`  
`collected.selectedPaymentMethod`

#### Errors
| name | description          |
|------|----------------------|
| MIN  | Amount below the min |
| MAX  | Amount above the max |
| API  | Error calling api    |

## API (JS/TS)

```shell
# Using yarn
$ yarn add @onramper/onramper-api

# Using npm
$ npm install @onramper/onramper-api
```

```javascript
import OnramperAPI from '@onramper/onramper-api'

async function getGateways() {
    let response
    try {
        response = await OnramperAPI.gateways()
    } catch (error) {
        return undefined
    }
    return response
}
```

#### Methods
##### gateways
`gateways = async (params: GatewaysParams, filter?: Filters): Promise<GatewaysResponse>`
##### rate
`rate = async (currency: string, crypto: string, amount: number, paymentMethod: string, params?: rateParams, signal?: AbortSignal): Promise<RateResponse>`
##### executeStep
`executeStep = async (step: NextStep, data: { [key: string]: any } | File): Promise<NextStep>`