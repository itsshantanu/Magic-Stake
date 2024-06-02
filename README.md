# Magic Staking Contracts

This repository contains Solidity smart contracts for a cross-chain staking system using Chainlink CCIP. The system includes sender, receiver, and staker contracts designed to handle USDC tokens.

## Contracts

### Sender.sol
This contract facilitates sending USDC tokens from one blockchain to another using Chainlink CCIP. Key features:
- Setting and deleting receivers for destination chains.
- Setting gas limits for destination chains.
- Sending messages and transferring USDC to receivers on other chains.
- Withdrawing LINK and USDC tokens.

### Receiver.sol
This contract receives USDC tokens from another blockchain and processes staking operations. Key features:
- Setting and deleting senders for source chains.
- Receiving messages and USDC from other chains.
- Retrying failed messages.

### Staker.sol
This contract handles staking and redeeming of USDC tokens. Key features:
- Staking USDC tokens for a beneficiary.
- Redeeming staked USDC tokens.

## Usage

### Deployment
1. Deploy `Staker` contract on destination chain.
2. Deploy `Receiver` contract with the staker contract address destination chain.
3. Deploy `Sender` contract with the router, LINK, and USDC token addresses on source chain.

### Configuration
- Set receivers and senders for the respective chains using `setReceiverForDestinationChain` and `setSenderForSourceChain` functions.
- Configure gas limits for cross-chain transactions.

## Functions

### Sender
- `setReceiverForDestinationChain(uint64 _destinationChainSelector, address _receiver)`
- `setGasLimitForDestinationChain(uint64 _destinationChainSelector, uint256 _gasLimit)`
- `sendMessagePayLINK(uint64 _destinationChainSelector, address _beneficiary, uint256 _amount)`
- `withdrawLinkToken(address _beneficiary)`
- `withdrawUsdcToken(address _beneficiary)`

### Receiver
- `setSenderForSourceChain(uint64 _sourceChainSelector, address _sender)`
- `ccipReceive(Client.Any2EVMMessage calldata any2EvmMessage)`
- `retryFailedMessage(bytes32 messageId, address beneficiary)`

### Staker
- `stake(address _beneficiary, uint256 _amount)`
- `redeem()`
- `decimals()`

### Supported Chains

- Avalanche Fuji —> Ethereum sepolia

- Ethereum Sepolia —> Avalanche Fuji

### Supported token 

- USDC

### Deployed contract address

#### Avalanche Fuji —> Ethereum sepolia

- Avalanche Fuji sender contract address - [0x26fb3CfEa45B212C7A45690DcD5a7A764a37cF77](https://testnet.snowtrace.io/address/0x26fb3CfEa45B212C7A45690DcD5a7A764a37cF77)

- Ethereum Sepolia Staker contract address  - [0x48540A20e83Ec311F6492f918a93Bcfc714A09bd](https://sepolia.etherscan.io/address/0x48540A20e83Ec311F6492f918a93Bcfc714A09bd)

- Ethereum Sepolia Receiver contract address - [0x8543dA0a4F9959ED3b937230B4CC6822c4b8528E](https://sepolia.etherscan.io/address/0x8543dA0a4F9959ED3b937230B4CC6822c4b8528E)

#### Ethereum Sepolia —> Avalanche Fuji

- Ethereum Sepolia Sender contract address - [0xb63B9BAec9788979E6ABEBCA6c6E9712d48f569F](https://sepolia.etherscan.io/address/0xb63B9BAec9788979E6ABEBCA6c6E9712d48f569F)

- Avalanche Fuji Staker contract address - [0x82C0CC46d2d890354Ed99880d9B67AcCF39f2144](https://testnet.snowtrace.io/token/0x82C0CC46d2d890354Ed99880d9B67AcCF39f2144?chainId=43113)

- Avalanche Fuji Receiver contract address - [0x86446b899C07aaA1d76247eB84375c9Ed606EE6B](https://testnet.snowtrace.io/address/0x86446b899C07aaA1d76247eB84375c9Ed606EE6B)

## License
This project is licensed under the MIT License.
