# Foundry Introduction Project: **FundMe** 

## Summary

A simple fundable smart contract that keeps track of funders and allows the contract-owner to withdraw the funds, built for educational purposes during Cyfrin Updraft's [Foundry Fundamentals](https://updraft.cyfrin.io/courses/foundry) course, using Solidity and Foundry.

## Requirements

- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
  - You'll know you did it right if you can run `git --version` and you see a response like `git version x.x.x`
- [Foundry](https://getfoundry.sh/)
  - You'll know you did it right if you can run `forge --version` and you see a response like `forge 0.2.0 (816e00b 2023-03-16T00:05:26.396218Z)`

## Usage

### Deploying 

#### Deploy on Anvil's Local Node
```
forge script script/DeployFundMe.s.sol
```

#### Deploy on a provided testnet

```
forge script script/DeployFundMe.s.sol --rpc-url <TESTNET_RPC_URL> --private-key <DEV_ONLY_PRIVATE_KEY> --broadcast --verify --etherscan-api-key <ETHERSCAN_API_KEY>
```

#### Deploy on Anvil using Foundry keystore 

```
forge script script/DeployFundMe.s.sol --rpc-url http://127.0.0.1:8545 --broadcast --account ANVIL_DEV
```

### Testing

#### Run test suit

```
forge test
```

#### Run specific test

```
forge test --match-test <testFunctionName>
```

#### Run tests on a testnet

```
forge test --fork-url <TESTNET_RPC_URL>
```

#### Check Test Coverage

```
test coverage
```

### Interacting (using .env)

#### Fund the contract

```
cast send <FUNDME_CONTRACT_ADDRESS> "fund()" --value 0.1ether --private-key <DEV_ONLY_PRIVATE_KEY>
```

or

```
forge script script/Interactions.s.sol --rpc-url sepolia  --private-key <DEV_ONLY_PRIVATE_KEY>  --broadcast
```

#### Withdraw

```
cast send <FUNDME_CONTRACT_ADDRESS> "withdraw()" --private-key <DEV_ONLY_PRIVATE_KEY>
```

#### Get owner

```
cast call <FUNDME_CONTRACT_ADDRESS> "getOwner()"
```

#### Estimate Gas

```
forge snapshot
```

### Interacting (using Foundry keystore)

#### Get version

```
cast call 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512 "getVersion()"
```

#### Fund the contract

```
cast send 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512 "fund()" --value 0.1ether --account ANVIL_DEV
```

#### Get funder address

```
cast call 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512 "getFunder(uint256)" 0
```

#### Get amount funded

```
cast call 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512 "getAddressToAmountFunded(address)" <address>
```

### Interacting (using Interactions.s.sol)

```
forge test --match-test testUserCanFundInteraction -vvv
```