# Vue-truffle

This project is design to connect to Ethereum blockchain and interact with MetaMask to send transaction on smart contract.  

### Technical stack

#### Frontend
- Vue
- Vuex
- Vue-Router
- Web3(MetaMask)

#### UI
- Sass

#### Smart contract/Solidity
- [Truffle](./TRUFFLE.md)

### Install flow

#### Clone repo

```
git clone https://github.com/PortalNetwork/vue-truffle.git
cd vue-truffle
```

#### Install ganache

```
npm install -g ganache-cli
```

#### Install truffle

```
npm install -g truffle
```

#### Build repo

```
npm install
truffle compile
```

#### Start repo

Open a new console
```
ganache-cli
```

```
truffle migrate
```

#### Vue framework deploy

```
cd dapp
npm run deploy
```




## Reference

- ganache-cli: https://github.com/trufflesuite/ganache-cli
- truffle: https://github.com/trufflesuite/truffle