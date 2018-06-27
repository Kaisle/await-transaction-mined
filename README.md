# await-transaction-mined
Check whether an Ethereum transaction has been mined. 

Polls the blockchain every 500ms and returns a promise with the transaction receipt once mined. 

```node
const awaitTransactionMined = require ('await-transaction-mined');

(async() {
  var txHash = '0x6ee5d58c314d183f3ca70e2292b39dca5ae46141fe4e6b1da5b106dd506e589a';
  const minedTxReceipt = await awaitTransactionMined(txHash);
})();
```

Custom poll interval:

```node
const awaitTransactionMined = require ('await-transaction-mined');
const POLL_INTERVAL = 5000;

(async() {
  var txHash = '0x6ee5d58c314d183f3ca70e2292b39dca5ae46141fe4e6b1da5b106dd506e589a';
  const minedTxReceipt = await awaitTransactionMined(txHash, POLL_INTERVAL);
})();
