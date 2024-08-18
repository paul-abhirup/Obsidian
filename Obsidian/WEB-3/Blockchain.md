https://andersbrownworth.com/blockchain/
https://animagraffs.com/how-cryptocurrency-works
## State Management
![[Pasted image 20240818025615.png]]
Blockchains start off with a Genesis State when they launch. Bitcoin's genesis state happened in 2009 when the public network launched. Ethereum's Genesis State happened in 2015, when it launched.

Every transaction on a blockchain modifies the global state that is replicated across all nodes.

Since there are millions of transactions, transactions get grouped together in blocks, hence the name - Blockchain. These blocks are chained together in a cryptographically verifiable way so they are historically traceable. The current state of a network can be recalculated at any time by starting from the genesis block and transitioning the state according to each block's information up until now.

## Nodes

A blockchain network is managed autonomously through a [peer-to-peer](https://en.wikipedia.org/wiki/Peer-to-peer) distributed network of computer nodes. Without going into too much detail, you can simply think of each node in the network as keeping a copy of the global transaction ledger. Therefore, each node can individually verify and audit transactions happening on the network and ensure there was no illicit behavior.

Another type of node, called a [mining node](https://en.wikipedia.org/wiki/Bitcoin#Mining), is responsible for grouping together new transactions being made on a network into a block, verifying them, and proposing the block to be included onto the global ledger by everyone else. Mining is computationally hard, and very important to do securely, so miners whose blocks get accepted are given a token reward for their hard work.

**The use of a blockchain confirms that each unit of value was transferred only once, and the ingenious mechanisms put forth by Satoshi Nakamoto solved the long-standing decentralized [double-spending](https://en.wikipedia.org/wiki/Double-spending) problem.**

Hashing is a process that transforms input data (of any size) into a fixed-size string of characters.
 
Hash functions have several important properties:
- Deterministic: The same input will always produce the same output.
- Fast computation: The hash value can be quickly computed for any given data.
- Pre-image resistance: It should be computationally infeasible to reverse the hash function (i.e., find the original input given its hash output).
- Small changes in input produce large changes in output: Even a tiny change in the input should drastically change the hash output.
- Collision resistance: It should be computationally infeasible to find two different inputs that produce the same hash output.

## SHA-256
https://emn178.github.io/online-tools/sha256.html

```js
//SHA-256  using node.js

const crypto = require('crypto');

const input = "100xdevs";
const hash = crypto.createHash('sha256').update(input).digest('hex');

console.log(hash);

//output 
7bbdcc0c751662c94bb948b204b564747f76c424d813604b9bbca9f2a56e83f2
// every time we hash it will produce a diff output

```
'hex' --> we are usign the hex encoding["hexadecimal"]

## Proof of work

##### Input string that produces a SHA-256 hash starting with '00000'
```js
// Function to find an input string that produces a SHA-256 hash starting with '00000'

const crypto = require('crypto');

function findHashWithPrefix(prefix){
  let inputNonce = 0;
  while(true){
    let NonceStr = inputNonce.toString();
    let hash = crypto.createHash('sha256').update(NonceStr).digest('hex');
  if(hash.startsWith(prefix)){
    return {input: NonceStr,hash: hash}
  }
    inputNonce++;
  }
}
// Find and print the input string and hash
const result = findHashWithPrefix('00000');
console.log(`Input: ${result.input}`);
console.log(`Hash: ${result.hash}`);
```

#### Input string should start with 100xdevs
```js
// Function to find an input string that starts with "100xDevs" produces a SHA-256 hash starting with '00000'

const crypto = require('crypto');

function findHashWithPrefix(prefix){
  let inputNonce = 0;
  while(true){
    let NonceStr = "100xDevs" + inputNonce.toString();
    let hash = crypto.createHash('sha256').update(NonceStr).digest('hex');
  if(hash.startsWith(prefix)){
    return {input: NonceStr,hash: hash}
  }
    inputNonce++;
  }
}
// Find and print the input string and hash
const result = findHashWithPrefix('00000');
console.log(`Input: ${result.input}`);
console.log(`Hash: ${result.hash}`);
```
![[Pasted image 20240818134401.png]]



