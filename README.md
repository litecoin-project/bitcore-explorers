<img src="http://bitcore.io/css/images/module-explorer.png" alt="bitcore explorers" height="35">
# Blockchain APIs for bitcore

[![NPM Package](https://img.shields.io/npm/v/bitcore-explorers.svg?style=flat-square)](https://www.npmjs.org/package/bitcore-explorers)
[![Build Status](https://img.shields.io/travis/bitpay/bitcore-explorers.svg?branch=master&style=flat-square)](https://travis-ci.org/bitpay/bitcore-explorers)
[![Coverage Status](https://img.shields.io/coveralls/bitpay/bitcore-explorers.svg?style=flat-square)](https://coveralls.io/r/bitpay/bitcore-explorers)

A module for [litecore](https://github.com/litecoin-project/litecore) that implements HTTP requests to different Web APIs to query the state of the blockchain.

## Getting started

Be careful! When using this module, the information retrieved from remote servers may be compromised and not reflect the actual state of the blockchain.

```sh
npm install litecore-explorers
bower install litecore-explorers
```

### UTXOS

```javascript
var explorers = require('bitcore-explorers');
var insight = new explorers.Insight();

insight.getUtxos('mLitecoin...', function(err, utxos) {
  if (err) {
    // Handle errors...
  } else {
    // Maybe use the UTXOs to create a transaction
  }
});
```

You can optionally pass a minimum confirmation amount, and getUtxos will only return unspent transactions with at least that many confirmations.

```javascript
var explorers = require('bitcore-explorers');
var insight = new explorers.Insight();

insight.getUtxos({address: 'mLitecoin...', minconf: 5}, function(err, utxos) {
  if (err) {
    // Handle errors...
  } else {
    // UTXOs with at least 5 confirmations are here
  }
});
```

### Address

Get information about a Litecoin address:

```javascript
var explorers = require('bitcore-explorers');
var insight = new explorers.Insight();

insight.address('mLitecoin...', function(err, data) {
  if (err) {
    // Handle errors...
  } else {
    // Address information here
  }
});
```

You can also specify a "from" and "to" range, useful for paging through the transaction history of an address:

```javascript
var explorers = require('bitcore-explorers');
var insight = new explorers.Insight();

insight.address({address: 'mLitecoin...', from: 1000, to: 2000}, function(err, data) {
  if (err) {
    // Handle errors...
  } else {
    // Address information here
  }
});
```

### Blocks

Get information about recent blocks:

```javascript
var explorers = require('bitcore-explorers');
var insight = new explorers.Insight();

insight.getBlocks(function(err, blocks) {
  if (err) {
    // Handle errors...
  } else {
    //Recent block data here
  }
});
```

Get information about a specific block, by its blockhash:

```javascript
var explorers = require('bitcore-explorers');
var insight = new explorers.Insight();

insight.getBlock('369005760377532901c126ae4e907352f66624033275c92803f538773415792a', function(err, block) {
  if (err) {
    // Handle errors...
  } else {
    //Block data here
  }
});
```

### Broadcast a Transaction

```javascript
var explorers = require('bitcore-explorers');
var insight = new explorers.Insight();

insight.broadcast(tx, function(err, returnedTxId) {
  if (err) {
    // Handle errors...
  } else {
    // Mark the transaction as broadcasted
  }
});
```

## Contributing

See [CONTRIBUTING.md](https://github.com/bitpay/bitcore/blob/master/CONTRIBUTING.md) on the main bitcore repo for information about how to contribute.

## License

Code released under [the MIT license](https://github.com/bitpay/bitcore/blob/master/LICENSE).

Copyright 2013-2015 BitPay, Inc. Bitcore is a trademark maintained by BitPay, Inc.

[bitcore]: http://github.com/bitpay/bitcore-explorers
