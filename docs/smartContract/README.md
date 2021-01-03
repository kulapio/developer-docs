# Smart Contract

The core logic is programmed into smart contracts that exist on the Blockchain and the code is open-source so anyone can audit as well as create your own frontend implementation that can receiving a fee on each transaction occurred.

## Addresses

| Contract Name | Address                                    | Network |
|---------------|--------------------------------------------|---------|
| KULAPDex      | 0x3833cf2972394d636b1C5b80d34FeE1F17175b77 | Mainnet |

## Functions

The solidity `KULAPDex.sol` contract acts as a single endpoint of the system and contains the functions that allow users to initial the trade from one token to another token on the given best path that got from off-chain API.

### Trade Execution

```js
function trade(uint256 tradingProxyIndex, ERC20 src, uint256 srcAmount, ERC20 dest, uint256 minDestAmount, uint256 partnerIndex) → uint256
```

| Parameter         | Type    | Description                                |
|-------------------|---------|--------------------------------------------|
| tradingProxyIndex | uint256 | Given trading proxy ID from off-chain API  | 
| src               | ERC20   | Source ERC20 token address*                 |          
| srcAmount         | uint256 | Source ERC20 token amount in Wei           | 
| dest              | ERC20   | Destination ERC20 token address*            | 
| minDestAmount     | uint256 | Min. Destination ERC20 token amount in Wei |
| partnerIndex      | uint256 | Partner ID (Default : 0)                   | 

* 0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE for native ETH 

If the source token is ERC20 token, the user is required to call approve function to give an allowance to the `KULAPDex.sol` contract stats at the top of the section.

```js
ERC20token.approve( "0x3833cf2972394d636b1C5b80d34FeE1F17175b77" , srcAmount)
```

#### Returns ####

* uint256 - Conversion fee in Wei

## Events

Smart Contract can emit events that can be listened by applications to be notified when a contract has performed specific action which is helpful when finding aggregated information such as trading volumes, daily returns, volatility, etc.

### Trade

Emitted when a trade is executed.

```js
event Trade(address indexed srcAsset, uint256 srcAmount, address indexed destAsset, uint256 destAmount, address indexed trader, uint256 fee)
```

| Parameter   | Type     | Description                           |
|-------------|----------|---------------------------------------|
| srcAsset    | address  | Source ERC20 token address*           | 
| srcAmount   | uint256  | Source ERC20 token amount in Wei      | 
| destAsset   | address  | Destination ERC20 token address*      | 
| destAmount  | uint256  | Destination ERC20 token amount in Wei |
| trader      | address  | Adddess who executed the transaction  |
| fee         | uint256  | Fee that deduced from the trade       | 

* 0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE for native ETH 

### AddedTradingProxy

Emitted when the new trading proxy is registered to the system.

```js
event AddedTradingProxy(address indexed addedBy, string name, IKULAPTradingProxy indexed proxyAddress, uint256 indexed index)
```

| Parameter   | Type               | Description                 |
|-------------|--------------------|-----------------------------|
| addedBy     | address            | Address who added the proxy | 
| name        | string             | Name of the trading proxy   |          
| proxyAddress| IKULAPTradingProxy | Trading proxy address       | 
| index       | uint256            | Total trading proxies       | 

## Security

- v1 audited by Atato (November 2020) [Link](https://www.atato.com/wp-content/uploads/2020/11/Kulap-Security-Review.pdf)