## Polkadot.js JavaScript Library

![Selendra Polkadotjs](../assets/sel-pol.png "Selendra Polkadotjs")
### Introduction
The [Polkadot.js](https://polkadot.js.org/docs/api/start) library provide application developers a set of tools to interact with Selendra Nodes using Javascript, similar to web3.js on Ethereum. 

### Setup Polkadot.js with Selendra

To get started with the Polkadot.js library, we first need to install it using the following command:
```
yarn add @polkadot/api
```
Once done, the simplest setup to start using the library and its methods is the following:
```
const { ApiPromise, WsProvider } = require('@polkadot/api');
const { Keyring } = require('@polkadot/keyring');

const dest = 'destination account';
const sender = 'sender Seed';
const amount = 'Sending amount';

 const provider = new WsProvider('wss://rpc-testnet.selendra.org');

    // Create the API and wait until ready
    const api = await ApiPromise.create({ provider });

    // Constuct the keying after the API (crypto has an async init)
    const keyring = new Keyring({ type: 'sr25519' });

    const senderKey = keyring.addFromMnemonic(sender);

    // Get Chain Decimalse from node
    const decimals = api.registry.chainDecimals;

    // Create a extrinsic, transferring amount units to dest in xx amount
    const transfer = api.tx.balances.transfer(dest, (BigInt(amount * (10 ** decimals))));

    // Sign and send the transaction using our account
    const hash = await transfer.signAndSend(senderKey);

    console.log(hash.toHex());

```
Different methods are available inside provider and wallet. Depending on which network you want to connect to, you can set the RPC_URL to the following values:

- Indracore standalone node (default): http://127.0.0.1:9944
- Indracore TestNet: https://rpc.testnet.selendra.org

### Step-by-step Tutorials
In the case that you are interested in a more detailed step-by-step guide, you can go to [Developer documentation](https://polkadot.js.org/docs) for all (most?) of the libraries under the polkadot-js umbrella. If you want to build, this is where to start.