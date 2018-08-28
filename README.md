# await-transaction-mined
Check whether an Ethereum transaction has been mined. 

Polls the blockchain every 500ms and returns a promise with the transaction receipt once mined.

Can also ensure that the transaction is valid and final by waiting for 12 block confirmations once mined.

### Installation:

```node
npm install await-transaction-mined --save
```

### Example (using Infura and Ropsten):

```node
const awaitTransactionMined = require ('await-transaction-mined');
const Web3 = require('web3');
const web3 = new Web3(new Web3.providers.HttpProvider('https://ropsten.infura.io/'+<YOUR_INFURA_API_KEY>));

(async function() {
  var txHash = '0x6ee5d58c314d183f3ca70e2292b39dca5ae46141fe4e6b1da5b106dd506e589a';
  const minedTxReceipt = await awaitTransactionMined.awaitTx(web3, txHash);
})();
```
```node
console.log(minedTxReceipt);
```

```JAVASCRIPT
{ blockHash:
   '0xb624235c0577cbe38ba7957e96517872cd309dbbb748edece879f1f0aa376401',
  blockNumber: 3524686,
  contractAddress: null,
  cumulativeGasUsed: 4873733,
  from: '0x81b7e08f65bdf5648606c89998a9cc8164397647',
  gasUsed: 21000,
  logs: [],
  logsBloom:
   '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000',
  status: true,
  to: '0x929d50311e504dbdadaddb2e64a0383f5e7d36da',
  transactionHash:
   '0xfd10e323bbbe6a70aae6bbc2d19dbc16ba1f75ae5193df2aa9a177f015a07e39',
  transactionIndex: 56 }
```

#### Ensure transaction is final and has not ended up in an uncle block (waits for 12 block confirmations):

```node
const awaitTransactionMined = require ('await-transaction-mined');
const Web3 = require('web3');
const web3 = new Web3(new Web3.providers.HttpProvider('https://ropsten.infura.io/'+<YOUR_INFURA_API_KEY>));
const POLL_INTERVAL = 5000;

(async function() {
  var txHash = '0x6ee5d58c314d183f3ca70e2292b39dca5ae46141fe4e6b1da5b106dd506e589a';
  const minedTxReceipt = await awaitTransactionMined.awaitTx(web3, txHash, {ensureNotUncle: true});
})();
```

#### Custom poll interval:

```node
const awaitTransactionMined = require ('await-transaction-mined');
const Web3 = require('web3');
const web3 = new Web3(new Web3.providers.HttpProvider('https://ropsten.infura.io/'+<YOUR_INFURA_API_KEY>));
const POLL_INTERVAL = 5000;

(async function() {
  var txHash = '0x6ee5d58c314d183f3ca70e2292b39dca5ae46141fe4e6b1da5b106dd506e589a';
  const minedTxReceipt = await awaitTransactionMined.awaitTx(web3, txHash, {interval: POLL_INTERVAL});
})();
```

#### Custom blocks numbers confirmation number:

```node
const awaitTransactionMined = require ('await-transaction-mined');
const Web3 = require('web3');
const web3 = new Web3(new Web3.providers.HttpProvider('https://ropsten.infura.io/'+<YOUR_INFURA_API_KEY>));
const BLOCKS_NUMBER = 6;

(async function() {
  var txHash = '0x6ee5d58c314d183f3ca70e2292b39dca5ae46141fe4e6b1da5b106dd506e589a';
  const minedTxReceipt = await awaitTransactionMined.awaitTx(web3, txHash, {blocksToWait: BLOCKS_NUMBER});
})();
```
