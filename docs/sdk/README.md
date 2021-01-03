# SDK

KULAP SDK provides access to KULAP DEX from a custom application where the best rate will be given to you and your user on each trade using ERC-20 tokens.

## Initialization

Install the SDK using npm or yarn

```sh
yarn add kulap-sdk
```

You will need to the provider object to the constructor which will allows the SDK to automatically handle query and retrieve requests from blockchains the user is connected to. Also the access token doesn't required at the moment.

#### Node.js

```js
const { Kulap } = require("kulap-sdk")
const Web3 = require('web3')

const web3 = new Web3(new Web3.providers.HttpProvider("https://mainnet.infura.io/v3/YOUR_PROJECT_ID"))

const kulapSDK = new Kulap('access_key',web3.currentProvider) // getting access key from the kulap.io console
```

#### ES6 / Typescript with injected Web3 (Metamask)

```ts
import { Kulap } from "kulap-sdk"

const kulapSDK = new Kulap('access_key', window.ethereum) // getting access key from the kulap.io console
```

## Usage

#### To retrieve the list all available tokens
```js
const symbols = kulapSDK.listSymbols()
```

#### To get network ID
```js
const networkId = await kulapSDK.getNetworkId()
```

#### To get the rate of a token pair 

This will help construct the order details from the pair and given amount that later you use it for validate, approve and execute a trade.

```js
const srcToken = "ETH"
const destToken = "DAI"
const amountIn = "1" // 1 ETH

const order = await kulapSDK.getRate(baseToken, pairToken, amountIn)
```
##### Response
| Value      | Description                                |
|------------|--------------------------------------------|
| rate       | Best rate given from off-chain API         | 
| routes     | Trading proxy containing the best rate     |          
| fromAmount | Source ERC20 token amount in Wei           | 
| fromSymbol | Source token symbol                        | 
| toAmount   | Destination ERC20 token amount in Wei      |
| toSymbol   | Destination token symbol                   | 
| gasOptions | GAS price options (SLOW, STD, FAST)        | 

#### To get the allowance of an ERC20
```js
const isValidated = await kulapSDK.validate(response) // given response when get the rate 

// or

const fromSymbol = "DAI"
const fromAmount = "100" // 100 DAI
const isValidated = await kulapSDK.validate({ fromSymbol, fromAmount })
```

#### To approve an ERC20
```js
await kulapSDK.approve(order) // given response when get the rate 

// or

await kulapSDK.approve(order, { gasOptions : "FAST" }) // "FAST", "STD", "SLOW" (default : "FAST")

// or

const fromSymbol = "LINK"
await kulapSDK.approve({ fromSymbol }, { gasOptions : "SLOW" })
```

#### Execute trade

We would recommend to set the slippage rate to prevent surge, for example the default value is 0%, if the price is change more than the given price from order details, the transaction will failed.

```js
await kulapSDK.trade(order)

// or

await kulapSDK.trade(order , { gasOptions : "FAST", slippage : 3  }) // slippage must be provided in percentage 3 is 3%
```

If you registered as partner and want the commision to be paid out on transactions, kindly provide your partner id as following:
```js
await kulapSDK.trade(order, { partnerId : YOUR_ID })
```


### Gas price
 
There will be 3 options for gas price that being calculated from off-chain API that you can easily provide at the configuration when execute trade and/or approve functions. The default value is FAST.

| Key  | Description | Est. confirmation time |
|------|-------------|------------------------|
| FAST | fast        | < 2 minutes            |
| STD  | standard    | < 5 minutes            |
| SLOW | slow        | ~ 10 minutes           |
