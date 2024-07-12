## How to get all pool from Sun.io

### v1

FactoryV1: `TXk8rQSAvPvBBNtqSoY6nCfsXWCSSpTVQF`
step1: get the num of all reservetoken
```
    FactoryV1.tokenCount()
    return the number of reservetoken
```
step2: get the reservetoken address by traversal the tokenCount number
```
    FactoryV1.getTokenWithId(index)
    index = 0 ~ tokenCount
```
step3: get get the pool address by reservetoken 

```
    FactoryV1.getExchange(reservetoken)
    return the pool addrss
```
### v2
FactoryV2: `TKWJdrQkqHisa1X8HUdHEfREvTzw4pMAaY`

step1: get the num of all pools
```
    FactoryV2.allPairsLength()
    return the number of pools
```
step2: get the pool address by traversal the poollength number
```
    FactoryV2.allPairs(index)
    index = 0 ~ allPairsLength
```
### v3
FactoryV3: `TThJt8zaJzJMhCEScH7zWKnp5buVZqys9x`

step1: get the num of all pools
```
    FactoryV3.allPairsLength()
    return the number of pools
```
step2: get the pool address by traversal the poollength number
```
    FactoryV3.allPairs(index)
    index = 0 ~ allPairsLength
```