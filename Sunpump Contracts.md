# Sunpump Contracts

### LaunchpadProxy: TTfvyrAz86hbZk5iDpKD78pqLGgi8C7AAw (Bonding Curve Period)

\*\* ABI code to get from: [implementation address](https://tronscan.org/#/contract/TQHj5QZA8PaHBcAGkYdi8QxdtuNabuVx5r/code) 

#### **1\. createAndInitPurchase Function**

**Description:**

* This function allows the creation of a new token and immediately initiates a purchase of the token.

**Function Signature:**

```
function createAndInitPurchase(string memory name, string memory symbol) external payable nonReentrant onlyActive
```

**Parameters:**

* `name`: The name of the token to be created.  
* `symbol`: The symbol of the token to be created.

**TRX Requirement:**

* You must send a minimum of `mintFee` TRX as the call value for minting the token.

**Example Call:**

* Note that: there is a 20 TRX create token fee  
* In this example, 80 TRX \- 1% fee will be use for initial purchase of the token

```javascript
const tronWeb = require('tronweb');
const contractAddress = 'TTfvyrAz86hbZk5iDpKD78pqLGgi8C7AAw';

const name = 'MyToken';
const symbol = 'MTK';
const callValue = 100 * 1e6; // 100 TRX, adjust based on the required mintFee

const createAndInitPurchase = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    await contract.createAndInitPurchase(name, symbol).send({
        callValue: callValue
    });
};

createAndInitPurchase();
```

---

#### **2\. purchaseToken Function**

**Description:**

* This function allows you to purchase tokens by sending TRX.

**Function Signature:**

```
function purchaseToken(address token, uint256 AmountMin) public payable nonReentrant onlyActive
```

**Parameters:**

* `token`: The address of the token to purchase.  
* `AmountMin`: The minimum amount of tokens you expect to receive from the purchase.

**TRX Requirement:**

* You must send at least `minTxFee` TRX as the call value for the purchase.

**Related Helper Function:**

* **`getTokenAmountByPurchaseWithFee`**: Use this function to calculate the estimated amount of tokens and fee before purchasing.

**Example Call:**

```javascript
const tokenAddress = 'YourTokenAddress'; // Replace with your token address
const minTokensExpected = 1000 * 1e6; // Adjust based on the minimum tokens expected

const purchaseToken = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    const trxAmount = 50 * 1e6; // 50 TRX, adjust as needed
    await contract.purchaseToken(tokenAddress, minTokensExpected).send({
        callValue: trxAmount
    });
};

purchaseToken();
```

---

#### **3\. saleToken Function**

**Description:**

* This function allows you to sell your tokens in exchange for TRX.

**Function Signature:**

```
function saleToken(address token, uint256 tokenAmount, uint256 AmountMin) external nonReentrant onlyActive
```

**Parameters:**

* `token`: The address of the token to sell.  
* `tokenAmount`: The amount of tokens you want to sell.  
* `AmountMin`: The minimum amount of TRX you expect to receive from the sale.

**Related Helper Function:**

* **`getTrxAmountBySaleWithFee`**: Use this function to calculate the estimated amount of TRX and fee before selling.

**Example Call:**

```javascript
const tokenAddress = 'YourTokenAddress'; // Replace with your token address
const tokensToSell = 1000 * 1e6; // Amount of tokens to sell, adjust as needed
const minTrxExpected = 50 * 1e6; // Adjust based on the minimum TRX expected

const saleToken = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    await contract.saleToken(tokenAddress, tokensToSell, minTrxExpected).send();
};

saleToken();
```

---

#### **4\. getPrice Function**

**Description:**

* This function returns the current price of the token in TRX.

**Function Signature:**

```
function getPrice(address token) external view returns (uint256)
```

**Parameters:**

* `token`: The address of the token to query.

**Example Call:**

```javascript
const tokenAddress = 'YourTokenAddress'; // Replace with your token address

const getPrice = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    const price = await contract.getPrice(tokenAddress).call();
    console.log('Current Price:', price);
};

getPrice();
```

---

#### **5\. getTokenState Function**

**Description:**

* This function returns the current state of the token.

**Function Signature:**

```
function getTokenState(address token) public view returns (uint256)
```

**Parameters:**

* `token`: The address of the token to query.

**Example Call:**

```javascript
const tokenAddress = 'YourTokenAddress'; // Replace with your token address

const getTokenState = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    const state = await contract.getTokenState(tokenAddress).call();
    console.log('Token State:', state);
};

getTokenState();
```

---

#### **6\. getTokenAmountByPurchaseWithFee Function**

**Description:**

* This function estimates the token amount you will receive and the associated fee when purchasing tokens.

**Function Signature:**

```
function getTokenAmountByPurchaseWithFee(address token, uint256 trxAmount) public view returns (uint256 tokenAmount, uint256 fee)
```

**Parameters:**

* `token`: The address of the token to query.  
* `trxAmount`: The amount of TRX you plan to spend.

**Example Call**:

```javascript
const tokenAddress = 'YourTokenAddress'; // Replace with your token address
const trxAmount = 50 * 1e6; // 50 TRX, adjust as needed

const getTokenAmountByPurchaseWithFee = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    const { tokenAmount, fee } = await contract.getTokenAmountByPurchaseWithFee(tokenAddress, trxAmount).call();
    console.log('Estimated Tokens:', tokenAmount, 'Fee:', fee);
};

getTokenAmountByPurchaseWithFee();
```

---

#### **7\. getExactTokenAmountForPurchaseWithFee Function**

**Description:**

* This function calculates the exact amount of TRX required to purchase a specific token amount and the associated fee.

**Function Signature:**

```
function getExactTokenAmountForPurchaseWithFee(address token, uint256 tokenAmount) public view returns (uint256 trxAmount, uint256 fee)
```

**Parameters:**

* `token`: The address of the token to query.  
* `tokenAmount`: The exact amount of tokens you wish to purchase.

**Example Call:**

```javascript
const tokenAddress = 'YourTokenAddress'; // Replace with your token address
const tokenAmount = 1000 * 1e6; // Amount of tokens to purchase, adjust as needed

const getExactTokenAmountForPurchaseWithFee = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    const { trxAmount, fee } = await contract.getExactTokenAmountForPurchaseWithFee(tokenAddress, tokenAmount).call();
    console.log('Required TRX:', trxAmount, 'Fee:', fee);
};

getExactTokenAmountForPurchaseWithFee();
```

---

#### **8\. getTrxAmountBySaleWithFee Function**

**Description:**

* This function estimates the TRX amount you will receive and the associated fee when selling a specific amount of tokens.

**Function Signature:**

```
function getTrxAmountBySaleWithFee(address token, uint256 tokenAmount) public view returns (uint256 trxAmount, uint256 fee)
```

**Parameters:**

* `token`: The address of the token to query.  
* `tokenAmount`: The amount of tokens you wish to sell.

**Example Call:**

```javascript
const tokenAddress = 'YourTokenAddress'; // Replace with your token address
const tokenAmount = 1000 * 1e6; // Amount of tokens to sell, adjust as needed

const getTrxAmountBySaleWithFee = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    const { trxAmount, fee } = await contract.getTrxAmountBySaleWithFee(tokenAddress, tokenAmount).call();
    console.log('Estimated TRX:', trxAmount, 'Fee:', fee);
};

getTrxAmountBySaleWithFee();
```

---

#### **9\. getExactTrxAmountForSaleWithFee Function**

**Description:**

* This function calculates the exact amount of tokens required to obtain a specific TRX amount and the associated fee.

**Function Signature:**

```
function getExactTrxAmountForSaleWithFee(address token, uint256 trxAmount) public view returns (uint256 tokenAmount, uint256 fee)
```

**Parameters:**

* `token`: The address of the token to query.  
* `trxAmount`: The exact amount of TRX you wish to receive.

**Example Call:**

```javascript
const tokenAddress = 'YourTokenAddress'; // Replace with your token address
const trxAmount = 50 * 1e6; // Amount of TRX to receive, adjust as needed

const getExactTrxAmountForSaleWithFee = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    const { tokenAmount, fee } = await contract.getExactTrxAmountForSaleWithFee(tokenAddress, trxAmount).call();
    console.log('Required Tokens:', tokenAmount, 'Fee:', fee);
};

getExactTrxAmountForSaleWithFee();

```

### PumpSwapRouter: TZFs5ch1R1C4mmjwrrmZqeqbUgGpxY1yWB (Launched to Dex)

\*\* Only Allow Pump created token and TRX trading pair, using **[Sunpump Contracts](https://docs.google.com/document/d/1Xs3CP-MF9gz639CdIo_FCO2IKIADrtJ5MdCqEk4S7NM/edit#heading=h.8ohmkvc6ukgh)** to determine if a pair is allowed for trade. Else transaction will revert.  
\*\* Use the [Factory Contract](https://tronscan.org/#/contract/TKWJdrQkqHisa1X8HUdHEfREvTzw4pMAaY/code) to getPair address, then from the Pair address getReserves for token0 & token1  
\*\* Contract ABIs are available on TronScan

#### **1\. swapExactETHForTokens Function**

**Description:** This function swaps an exact amount of ETH for as many output tokens as possible, along the route determined by the path.

**Function Signature:**

```
function swapExactETHForTokens(uint amountOutMin, address[] calldata path, address to, uint deadline) external payable returns (uint[] memory amounts)
```

**Parameters:**

* `amountOutMin`: The minimum amount of output tokens that must be received for the transaction not to revert.  
* `path`: An array of token addresses. path.length must be at least 2\. Pools for each consecutive pair of addresses must exist and have liquidity.  
* `to`: Address to receive the output tokens.  
* `deadline`: Unix timestamp after which the transaction will revert.

TRX Requirement: This function requires you to send ETH as the call value, which will be swapped for the tokens.

**Example Call:**

```javascript
const tronWeb = require('tronweb');
const contractAddress = 'TZFs5ch1R1C4mmjwrrmZqeqbUgGpxY1yWB';

const amountOutMin = 100 * 1e6; // Example minimum amount of tokens to receive
const path = ['TOKEN_A_ADDRESS_HERE', 'TOKEN_B_ADDRESS_HERE']; // Example path
const to = 'TYourAddressHere';
const deadline = Math.floor(Date.now() / 1000) + 60 * 20; // 20 minutes from the current Unix time

const swapExactETHForTokens = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    await contract.swapExactETHForTokens(amountOutMin, path, to, deadline).send({
        callValue: tronWeb.toSun(1) // Example: sending 1 TRX
    });
};

swapExactETHForTokens();
```

#### **2\. swapTokensForExactETH Function**

**Description:** This function swaps an exact amount of tokens for as much ETH as possible.

**Function Signature:**

```
function swapTokensForExactETH(uint amountOut, uint amountInMax, address[] calldata path, address to, uint deadline) external returns (uint[] memory amounts)
```

**Parameters:**

* `amountOut`: The exact amount of ETH to receive.  
* `amountInMax`: The maximum amount of input tokens that can be required before the transaction reverts.  
* `path`: An array of token addresses. The first address must be the input token, and the last address must be WETH.  
* `to`: Address to receive the ETH.  
* `deadline`: Unix timestamp after which the transaction will revert.

**Example Call:**

```javascript
const amountOut = tronWeb.toSun(1); // 1 TRX
const amountInMax = 200 * 1e6; // Example maximum amount of tokens to send
const path = ['TOKEN_A_ADDRESS_HERE', 'TOKEN_B_ADDRESS_HERE']; // Example path
const to = 'TYourAddressHere';
const deadline = Math.floor(Date.now() / 1000) + 60 * 20; // 20 minutes from the current Unix time

const swapTokensForExactETH = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    await contract.swapTokensForExactETH(amountOut, amountInMax, path, to, deadline).send();
};

swapTokensForExactETH();
```

#### **3\. swapExactTokensForETH Function**

**Description:** This function swaps an exact amount of tokens for as much ETH as possible.

**Function Signature:**

```
function swapExactTokensForETH(uint amountIn, uint amountOutMin, address[] calldata path, address to, uint deadline) external returns (uint[] memory amounts)
```

**Parameters:**

* `amountIn`: The exact amount of input tokens to send.  
* `amountOutMin`: The minimum amount of ETH that must be received for the transaction not to revert.  
* `path`: An array of token addresses. The first address must be the input token, and the last address must be WETH.  
* `to`: Address to receive the ETH.  
* `deadline`: Unix timestamp after which the transaction will revert.

**Example Call:**

```javascript
const amountIn = 200 * 1e6; // Example amount of tokens to send
const amountOutMin = tronWeb.toSun(0.5); // Example minimum amount of ETH to receive
const path = ['TOKEN_A_ADDRESS_HERE', 'TOKEN_B_ADDRESS_HERE']; // Example path
const to = 'TYourAddressHere';
const deadline = Math.floor(Date.now() / 1000) + 60 * 20; // 20 minutes from the current Unix time

const swapExactTokensForETH = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    await contract.swapExactTokensForETH(amountIn, amountOutMin, path, to, deadline).send();
};

swapExactTokensForETH();
```

#### **4\. swapETHForExactTokens Function**

**Description:** This function swaps an exact amount of ETH for as few input tokens as possible.

**Function Signature:**

```
function swapETHForExactTokens(uint amountOut, address[] calldata path, address to, uint deadline) external payable returns (uint[] memory amounts)
```

**Parameters:**

* `amountOut`: The exact amount of tokens to receive.  
* `path`: An array of token addresses. The first address must be WETH, and the last address must be the output token.  
* `to`: Address to receive the tokens.  
* `deadline`: Unix timestamp after which the transaction will revert.

TRX Requirement: This function requires you to send ETH as the call value, which will be swapped for the tokens.  
**Example Call:**

```javascript
const amountOut = 200 * 1e6; // Example amount of tokens to receive
const path = ['TOKEN_A_ADDRESS_HERE', 'TOKEN_B_ADDRESS_HERE']; // Example path
const to = 'TYourAddressHere';
const deadline = Math.floor(Date.now() / 1000) + 60 * 20; // 20 minutes from the current Unix time

const swapETHForExactTokens = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    await contract.swapETHForExactTokens(amountOut, path, to, deadline).send({
        callValue: tronWeb.toSun(1) // Example: sending 1 TRX
    });
};

swapETHForExactTokens();
```

#### **5\.  getAmountOut Function**

**Description:** This function calculates the maximum output amount of a token given an input amount of another token.

**Function Signature:**

```
function getAmountOut(uint amountIn, uint reserveIn, uint reserveOut) external pure returns (uint amountOut)
```

**Parameters:**

* `amountIn`: The amount of input tokens.  
* `reserveIn`: The reserve of the input token in the pair.  
* `reserveOut`: The reserve of the output token in the pair.

**Example Call:**

```javascript
const amountIn = 100 * 1e6; // Example input amount
const reserveIn = 500 * 1e6; // Example reserve of the input token
const reserveOut = 1000 * 1e6; // Example reserve of the output token

const getAmountOut = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    const amountOut = await contract.getAmountOut(amountIn, reserveIn, reserveOut).call();
    console.log('Output Amount:', amountOut);
};

getAmountOut();
```

#### **6\. getAmountIn Function**

**Description:** This function calculates the required input amount of a token given an output amount of another token.

**Function Signature:**

```
function getAmountIn(uint amountOut, uint reserveIn, uint reserveOut) external pure returns (uint amountIn)
```

**Parameters:**

* `amountOut`: The desired amount of output tokens.  
* `reserveIn`: The reserve of the input token in the pair.  
* `reserveOut`: The reserve of the output token in the pair.

**Example Call:**

```javascript
const amountOut = 100 * 1e6; // Example output amount
const reserveIn = 500 * 1e6; // Example reserve of the input token
const reserveOut = 1000 * 1e6; // Example reserve of the output token

const getAmountOut = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    const amountOut = await contract.getAmountIn(amountOut, reserveIn, reserveOut).call();
    console.log('Output Amount:', amountOut);
};
```

#### **7\. isAllowedTradingPair Function**

**Description**

The `isAllowedTradingPair` function determines whether a given trading pair of tokens is allowed for trading. This function is typically used to enforce trading policies or restrictions on specific pairs of tokens within a decentralized exchange or trading platform.

**Function Signature:**

```
function isAllowedTradingPair(address tokenA, address tokenB) external view returns (bool);
```

**Parameters:**

* `tokenA`: The address of the first token in the trading pair.  
* `tokenB`: The address of the second token in the trading pair.

**Example Call:**

```javascript
const contractAddress = 'YOUR_CONTRACT_ADDRESS_HERE';
const tokenA = 'TOKEN_A_ADDRESS_HERE'; // Replace with the address of token A
const tokenB = 'TOKEN_B_ADDRESS_HERE'; // Replace with the address of token B

const checkTradingPair = async () => {
    try {
        const contract = await tronWeb.contract(abi, contractAddress);
        const isAllowed = await contract.isAllowedTradingPair(tokenA, tokenB).call();
        console.log(`Trading pair (${tokenA}, ${tokenB}) allowed:`, isAllowed);
    } catch (error) {
        console.error('Error checking trading pair:', error);
    }
};

checkTradingPair();
```

### PumpSmartExchangeRouter: TSiiYf1b1PV1fpT9T7V4wy11btsNVajw1g (Launched to Dex)

#### **1.swapExactInput Function**

**Description**

The  `swapExactInput` function is the unified entrance for swaps.

**Function Signature:**

```
function swapExactInput(
        address[] calldata path,
        string[] calldata poolVersion,
        uint256[] calldata versionLen,
        uint24[] calldata fees,
        SwapData calldata data
    ) external nonReentrant payable returns (uint256[] memory amountsOut)

struct SwapData {
        uint256 amountIn;
        uint256 amountOutMin;
        address to;
        uint256 deadline;
    }
```

**Parameters:**

* `path`: The token address list for swap to.  
* `poolVersion`: The version list for pool‘s version for pathed token.  
* `versionLen`: The length list for pool’s length by version.  
* `fees`: The fees list for pool’s fees, just support the SUNSWAP V3 pools  
* `data`: The swap info ,Use `SwapData` Structure ,obtain token `amountIn`, min amountOut expect `amountOutMin` ,receiver `to`  and `deadline`

**Example Call:**

```javascript
const tronWeb = require('tronweb');
const contractAddress ='TSiiYf1b1PV1fpT9T7V4wy11btsNVajw1g
';

const amountOutMin =YOUR_TOKEN_AMOUNT_MIN; // Example minimum amount of tokens to receive
const pathTrxToToken = [address(0),WTRX,TokenAddress]; // Example path
const pathTokenToTrx = [tokenAddress,WTRX,address(0)];
const poolVersion = ["v2"];
const versionLen = ["3"];
const fees = [0,0,0];
const amountIn = YOUR_TOKEN_AMOUNT
const to = 'TYourAddressHere';
const deadline = Math.floor(Date.now() / 1000) + 60 * 20; // 20 minutes from the current Unix time
const swapdata = [amountIn,amountOutMin,to,deadline];
// trx - token
const swapExactInput = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    await contract.swapExactInput(
pathTrxToToken, 
poolVersion, 
versionLen, 
fees,
swapdata
).send({
        callValue: tronWeb.toSun(amountIn) // Example: sending 1 TRX
    });
};
// token -trx
const swapExactInput = async () => {
    const contract = await tronWeb.contract(abi, contractAddress);
    await contract.swapExactInput(
pathTokenToTrx, 
poolVersion, 
versionLen, 
fees,
swapdata
).send();
};
```

