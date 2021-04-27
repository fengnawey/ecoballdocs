# developers

>develop documents

## web3.js

The web3.js library is a collection of modules that contain functionality for the ethereum ecosystem.

- web3-eth is for the ethereum blockchain and smart contracts.
- web3-shh is for the whisper protocol, to communicate p2p and broadcast.
- web3-bzz is for the swarm protocol, the decentralized file storage.
- web3-utils contains useful helper functions for Dapp developers.

### Adding web3.js

First you need to get web3.js into your project. This can be done using the following methods:

- npm: npm install web3
- yarn: yarn add web3
- pure js: link the dist/web3.min.js

After that you need to create a web3 instance and set a provider.

Most Ethereum-supported browsers like MetaMask have an EIP-1193 compliant provider available at window.ethereum.

For web3.js, check Web3.givenProvider.

If this property is null you should connect to a remote/local node.

````
// In Node.js use: const Web3 = require('web3');

let web3 = new Web3(Web3.givenProvider || "ws://localhost:8545");

````

That’s it! Now you can use the web3 object.

### web3 api interface


#### web3

##### Web3.modules

##### version

##### utils

##### setProvider

##### providers

##### givenProvider

##### currentProvider

##### BatchRequest

##### extend

#### web3.eth

##### packages

**subscribe**

web3.eth.subscribe， reference [Subscribe reference documentation](https://web3js.readthedocs.io/en/v1.3.4/web3-eth-subscribe.html)。

**Contract**

web3.eth.Contract，reference [Contract reference documentation](https://web3js.readthedocs.io/en/v1.3.4/web3-eth-contract.html)。

**Iban**

web3.eth.Iban，reference [Iban reference documentation](https://web3js.readthedocs.io/en/v1.3.4/web3-eth-iban.html)。

**personal**

web3.eth.personal， reference [personal reference documentation](https://web3js.readthedocs.io/en/v1.3.4/web3-eth-personal.html)。

**accounts**

web3.eth.accounts，reference [accounts reference documentation](https://web3js.readthedocs.io/en/v1.3.4/web3-eth-accounts.html)。

**ens**

web3.eth.ens， reference [ENS reference documentation](https://web3js.readthedocs.io/en/v1.3.4/web3-eth-ens.html)。

**abi**

web3.eth.abi， reference [ABI reference documentation](https://web3js.readthedocs.io/en/v1.3.4/web3-eth-abi.html)。

**net**

web3.eth.net， reference [net reference documentation](https://web3js.readthedocs.io/en/v1.3.4/web3-eth-net.html)。

##### attribute and method


setProvider

providers

givenProvider

currentProvider

BatchRequest

extend

defaultAccount

defaultBlock

defaultHardfork

defaultChain

defaultCommon

transactionBlockTimeout

transactionConfirmationBlocks

transactionPollingTimeout

handleRevert

getProtocolVersion

isSyncing

getCoinbase

isMining

getHashrate

getGasPrice

getAccounts

getBlockNumber

getBalance

getStorageAt

getCode

getBlock

getBlockTransactionCount

getBlockUncleCount

getUncle

getTransaction

getPendingTransactions

getTransactionFromBlock

getTransactionReceipt

getTransactionCount

sendTransaction

sendSignedTransaction

sign

signTransaction

call

estimateGas

getPastLogs

getWork

submitWork

requestAccounts

getChainId

getNodeInfo

getProof


#### web3.eth.subscribe

#### web3.eth.Contract

##### usage
##### attribute

defaultAccount

defaultBlock

defaultHardfork

defaultChain

defaultCommon

transactionBlockTimeout

transactionConfirmationBlocks

transactionPollingTimeout

handleRevert

options.address

options.jsonInterface


##### mothod

clone

deploy

methods

methods.myMethod.call

methods.myMethod.send

methods.myMethod.estimateGas

methods.myMethod.encodeABI

##### event

once

events

events.allEvent

getPastEvents



#### web3.eth.accounts

create

privateKeyToAccount

signTransaction

recoverTransaction

hashMessage

sign

recover

encrypt

decrypt

wallet

wallet.create

wallet.add

wallet.remove

wallet.clear

wallet.encrypt

wallet.decrypt

wallet.save

wallet.load


#### web3.eth.personal


setProvider

providers

givenProvider

currentProvider

BatchRequest

extend

newAccount

sign

ecRecover

signTransaction

sendTransaction

unlockAccount

lockAccount

getAccounts

importRawKey



#### web3.eth.ens



registry

resolver

getAddress

setAddress

getPubkey

setPubkey

getContent

setContent

getMultihash

setMultihash

ENS events



#### web3.eth.Iban

#### web3.eth.abi

#### web3.*.net

#### web3.bzz

#### web3.shh

#### web3.utils

#### web3.eth.accounts

#### web3.eth.personal

#### web3.eth.ens

#### web3.eth.Iban

#### web3.eth.abi

#### web3.*.net

#### web3.bzz

#### web3.shh

#### web3.utils

