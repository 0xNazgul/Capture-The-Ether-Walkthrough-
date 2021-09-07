# Public Key

**HINT:** Research how transactions are signed on the blockchain(ECDSA and recovery id)
<details>
<summary>Answer</summary>
<p>

Look up ```0x92b28647ae1f3264661f72fb2eb9625a89d88a31``` on [ropsten.etherscan](https://ropsten.etherscan.io/) and grab the most recent transaction's raw transaction hex.
Use ethereumjs-tx to get the public key like so:

```js
const EthereumTx = require ('etehreumjs-tx');

const rawTx =
`0xf87080843b9aca0083015f90946b477781b0e68031109f21887e6b5afeaaeb002b808c5468616e6b732c206d616e2129a0a5522718c0f95dde27f0827f55de836342ceda594d20458523dd71a539d52ad7a05710e64311d481764b5ae8ca691b05d14054782c7d489f3511a7abf2f5078962`;

console.log('0x' + new EthereumTx(rawTx).getSenderPublicKey().toString('hex'));
console.log('0x' + new EthereumTx(rawTx).getSenderAddress().toString('hex'));

// OUTPUT: 0x613a8d23bd34f7e568ef4eb1f68058e77620e40079e88f705dfb258d7a06a1a0364dbe56cab53faf26137bec044efd0b07eec8703ba4a31c588d9d94c35c8db4
```
Go back to the contract and plug that into the function ```authenticate()```

</p>
</details>