# API

## Get Best Rate


```
GET https://api.kulap.io/v1/api/rate/best-rate/toAmount
```

### Request Parameters

| Name       | Description          | Example             | Required   |
|------------|----------------------|---------------------|------------|
| from       | Symbol           | ETH, DAI or WBTC    | ✔️          |
| to         | Symbol           | ETH, DAI or WBTC    | ✔️          |
| fromAmount | Amount in Wei format | 1000000000000000000 | ✔️        |
| accessKey  | Your access token     | xxxx                | ✔️          |
