---
title: Verify your smart contracts
lang: en-US
keywords: [morphism,ethereum,rollup,layer2,validity proof,optimstic zk-rollup]
description: Upgrade your blockchain experience with Morphism - the secure decentralized, cost0efficient, and high-performing optimstic zk-rollup solution. Try it now!
---

After deploying your smart contracts, it's important to verify your code on our [block explorer](explorer.testnet.morphism.xyz). This can be done in an automated way using your develop framework such as hardhat.



## Verify with develop framework

Most smart contract tooling has plugins for verifying your contracts easily on Etherscan. Blockscout supports Etherscan's contract verification APIs, and it's straight forward to use these tools with the Morphism Testnet.

### Hardhat

:::info

Use [harthat-verify plugin](https://hardhat.org/hardhat-runner/plugins/nomicfoundation-hardhat-verify)

:::

First run this under hardhat contract project directory:

~~~
yarn add --dev @nomiclabs/hardhat-etherscan
~~~

Then edit your 'hardhat.config.js' file to point to the Morphism testnet RPC & explorer
> hardhat.config.js


~~~

require("@nomiclabs/hardhat-waffle");
require("@nomiclabs/hardhat-etherscan");
require('hardhat-deploy');

module.exports = {
    ...
    networks: {
    tMorphism: {
      url: 'https://rpc.testnet.morphism.xyz ' || '',
      accounts:
        process.env.PRIVATE_KEY !== undefined ? [process.env.PRIVATE_KEY] : [],
     },
    },
    ...
    etherscan: {
        apiKey: {
          tMorphism: "abc",
        },
        customChains: [
          {
            network: "tMorphism",
            chainId: 2710,
            urls: {
              apiURL: "",
              browserURL: "https://explorer.testnet.morphism.xyz",
            },
          },
        ],
      }
}

~~~

When contract is deployed, adding a script: 
> scripts/lock.js

~~~
await hre.run("verify:verify", {
    address: contract.address, 
    constructorArguments: [xxx], 
});
~~~

Final step, execute

> NODE_ENV=devnet npx hardhat run scripts/lock.js --network devnet

To verify the contract code

## Vefiry with browser

TBD