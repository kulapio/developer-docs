# Smart Contract

## Addresses

The following are the contract addresses that are required to initiate interaction with the system.

| Address                                    | Network          |
|--------------------------------------------|------------------|
| 0x3833cf2972394d636b1C5b80d34FeE1F17175b77 | Ethereum Mainnet |

<!-- ERC20 tokens have to be approved before swapping them to the above address. -->

## Functions

The main entry point for the system is the solidity contract `KULAPDex.sol` which composed of functions which will be created to execute transactions.

### Trade Execution

```
function trade(uint256 tradingProxyIndex, ERC20 src, uint256 srcAmount, ERC20 dest, uint256 minDestAmount, uint256 partnerIndex) → uint256
```

| Parameter   | Type               | Description                 |
|-------------|--------------------|-----------------------------|
| addedBy     | address            | Address who added the proxy | 
| name        | string             | Name of the trading pair    |          
| proxyAddress| IKULAPTradingProxy | Trading proxy address       | 
| index       | uint256            | Total trading proxy         | 

If the source token is ERC20 token, the user is required to call approve function to give an allowance to the main smart contract stats at the top of the section.

#### Returns ####

TBA

#### Example ####

TBA





## Events

In Ethereum, Smart Contract can emit events that can be listened by applications to be notified when a contract has performed specific action which is helpful when finding aggregated information such as trading volumes, daily returns, volatility, etc.

### Trade

Emitted when a trade is executed.

```
event Trade(address indexed srcAsset, uint256 srcAmount, address indexed destAsset, uint256 destAmount, address indexed trader, uint256 fee)
```

| Parameter   | Type     | Description                           |
|-------------|----------|---------------------------------------|
| srcAsset    | address  | Source ERC20 token address            | 
| srcAmount   | uint256  | Source ERC20 token amount in Wei      | 
| destAsset   | address  | Destination ERC20 token address       | 
| destAmount  | uint256  | Destination ERC20 token amount in Wei |
| trader      | address  | Partner address (default : 0)         |
| fee         | uint256  | System fee                            | 

### AddedTradingProxy

Emitted when the new trading pair is added to the system.

```
event AddedTradingProxy(address indexed addedBy, string name, IKULAPTradingProxy indexed proxyAddress, uint256 indexed index)
```

| Parameter   | Type               | Description                 |
|-------------|--------------------|-----------------------------|
| addedBy     | address            | Address who added the proxy | 
| name        | string             | Name of the trading pair    |          
| proxyAddress| IKULAPTradingProxy | Trading proxy address       | 
| index       | uint256            | Total trading proxy         | 

## Security

- v1 audited by XXX (October 2020)