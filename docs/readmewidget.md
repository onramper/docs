#Onramper

This project is created using create-react-app with support for Typescript, here you will find some notes about how to customize or build the widget from the source files. Any doubt, ping `oxsalah` in Telegram.

Directory structure (only main files listed):  

```
widget
├── dist # generated after build
├── ...
├── src
│   ├── OnramperWidget
│   ├── ...
│   ├── App.tsx
│   ├── index.css
│   └── index.tsx 
├── ...
├── component.tsconfig.json
├── package.json
├── tsconfig.json
├── webpack.config.js
└── index.html
```

| File / folder                                             | Description                                                                                                                                   |
| --------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `./src/OnramperWidget`                                    | Source files of the widget. [See more.](#onramperwidget)                                                                                      |
| `./component.tsconfig.json`<br>`./webpack.config.js`      | Config files used to transpile/bundle the widget component.                                                                                   |
| `./src/App.tsx`<br>`./src/index.css`<br>`./src/index.tsx` | Base files that imports the OnramperWidget. `create-react-app` app entry files. Buy page source files.                                        |
| `./dist`                                                  | Bundled component ready for distribution.                                                                                                     |
| `./tsconfig.json`                                         | Typescript config file used by `create-react-app` app.                                                                                        |
| `./package.json`                                          | package.json file of the project, describes all the necesary for test, run and build the component, the buy page and the developement server. |
| `./index.html`                                            | Static website to test the final bundle (`./dist/index.js`).                                                                                  |

## Setup
Install dependencies
```shell
npm install
```

## Developement
Start developement server
```
npm start
```

## Build
The `build:component` script will transpile/bundle the widget component source files to the `./dist` folder

```shell
npm run build:component
```

## OnramperWidget
Directory structure (only main files listed):  

```
OnramperWidget
├── NavContext
├── ApiContext
│   ├── ...
│   └── api 
├── ...
├── steps
│   ├── ...
│   └── Step 
└── index.tsx
```

| File / folder      | Description                                                                                                                                                          |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `./NavContext`     | Navigation context. Manages the screens stack. Exposes functions to navigate between screens. [See more.](#navcontext)                                               |
| `./ApiContext`     | Api context. Manages the state of the app and the API calls. Exposes functions to make requests to the api and to manage the general state. [See more.](#apicontext) |
| `./ApiContext/api` | Module that handles the API calls. Includes types for the different api calls. [See more.](#onramperwidget)                                                          |
| `./steps`          | Folder that contains the diferent screens components.                                                                                                                |
| `./steps/Step`     | General step component. Used to redirect and display the correct screen according to the next step get from the API. [See more.](#onramperwidget)                    |
| `./index.tsx`      | Exports the widget component.                                                                                                                                        |

#### NavContext
Navigation context. Manages the screens stack and exposes functions to navigate between screens. Learn about contexts in React [here](https://reactjs.org/docs/context.html).

Exports `NavContext`, `NavProvider` and `NavContainer`.

`NavProvider`: Navigation provider. Wraps the components that consume the context.
`NavContainer`: Wraps the main screen. [See implementation here](./index.tsx).  
`NavContext`: Navigation context.

Functions availables to consume:  

| Function                                 | Description                                          |
| ---------------------------------------- | ---------------------------------------------------- |
| `nextScreen(screen: React.ReactNode)`    | Adds `screen` to the top of the screens stack.       |
| `backScreen()`                           | Removes the top screen of the stack.                 |
| `onlyScreen(screen: React.ReactNode)`    | Removes all screens and adds `screen` to the stack.. |
| `replaceScreen(screen: React.ReactNode)` | Replaces the top screen of the stack by `screen`.    |

#### ApiContext
Api context. Manages the state of the widget and the API responses. Exposes functions and variables to manage the general state and to make requests to the [api](https://docs.onramper.dev/API-Reference/).  
Learn more about contexts [here](https://reactjs.org/docs/context.html).

Consuming the api context you can access to 4 general objects: `apiInterface`, `data`, `inputInterface`, `collected`.

###### apiInterface
| Function/variable                                        | Description                                                                                                                                                                         |
| -------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| apiInterface.init(country?: string)                      | Makes an initial call to get all the options the user have to buy crypto given a country (if `country` is not set, is automatically detected by the api by the user's IP)           |
| apiInterface.executeStep(step: NextStep, params: object) | Sends to the api the step with the corresponding step fields filled (`params`). Returns a new step or throws an error if there is any error in the fields the user input (`params`) |
| apiInterface.getRates()                                  | Gets available gateways rates and stores it in `data` object (see below)                                                                                                            |

###### data
| Function/variable                                                                                                                                        | Description                                                                                                                                                                         |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data.handleCryptoChange(crypto?: ItemType)<br>data.handleCurrencyChange(currency?: ItemType)<br>data.handlePaymentMethodChange(paymentMethod?: ItemType) | Makes an initial call to get all the options the user have to buy crypto given a country (if `country` is not set, is automatically detected by the api by the user's IP)           |
| apiInterface.executeStep(step: NextStep, params: object)                                                                                                 | Sends to the api the step with the corresponding step fields filled (`params`). Returns a new step or throws an error if there is any error in the fields the user input (`params`) |
| apiInterface.getRates()                                                                                                                                  | Gets available gateways rates and stores it in `data` object (see below)                                                                                                            |


##### Data Interface
`data.handleCryptoChange(crypto?: ItemType)`  
`data.handleCurrencyChange(currency?: ItemType)`  
`data.handlePaymentMethodChange(paymentMethod?: ItemType)`

##### Input Interface
`inputInterface.handleInputChange(name: string, value: any)`

##### Collected Interface
`collected.amount`  
`collected.selectedCrypto`  
`collected.selectedCurrency`  
`collected.selectedPaymentMethod`