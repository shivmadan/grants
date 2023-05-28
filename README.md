# Grants
Autonomous grant payment application

# Stake and pay contract with Chainlink API or Etherscan API

1/ This contract allows a user to stake a certain amount of tokens (specified by minimumStake), and then automatically pays out a certain amount of tokens (specified by rewardRate) based on the price data obtained from the specified oracle API endpoint (oracle). 

2/ The contract uses the Chainlink AggregatorV3Interface to obtain the price data.

3/ The stake function allows a user to stake their tokens, and the unstake function allows them to unstake them. The claim function allows the user to claim their rewards based on the elapsed time since the last claim and the current price data obtained from the oracle API endpoint.

4/ The contract stores the staked balances of each user in the balances mapping, and the timestamp of their last claim in the lastClaimed mapping. It also stores whether or not a user has staked in.  It keeps track of stake and reward balances separately for each user using the Stake struct and the stakes mapping. When a user claims their rewards.

# Code Overview

This Solidity code represents a staking contract that allows users to stake a specific token and earn rewards based on their staked balance. The contract uses Chainlink's AggregatorV3Interface for fetching price data from an external oracle to calculate the rewards.

## Prerequisites
- Solidity compiler version 0.8.0 or higher
- Chainlink's AggregatorV3Interface contract (imported from "https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.8/interfaces/AggregatorV3Interface.sol")

## Contract Overview
The StakingContract contract consists of the following key functionalities:

### Stake Struct
- The `Stake` struct stores information related to a user's stake, including their balance, last claimed timestamp, reward balance, and stake status.

### State Variables
- `stakes`: A mapping that stores user addresses as keys and their respective `Stake` struct as values.
- `minimumStake`: A constant defining the minimum required stake amount.
- `rewardRate`: A constant representing the rate at which rewards are calculated.
- `claimInterval`: A constant specifying the time interval required between two consecutive claims.
- `token`: An immutable address representing the token being staked.
- `oracle`: An immutable address representing the oracle contract providing price data.
- `priceDecimals`: An immutable uint256 storing the decimal places of the price feed.
- `rewardRecipients`: An array containing addresses of users who have received rewards.
- `rewardIndices`: A mapping that stores the index of each user's reward in the `rewardRecipients` array.

### Constructor
- The constructor function initializes the contract by setting the `token` and `oracle` addresses and fetching the `priceDecimals` from the Chainlink oracle.

### Stake
- The `stake` function allows users to stake a specific amount of the token. It requires the staked amount to be equal to or greater than the minimum stake. The staked amount is transferred from the user's address to the contract, and the user's stake information is updated.

### Unstake
- The `unstake` function allows users to withdraw their staked amount from the contract. The staked amount is transferred from the contract back to the user's address, and the user's stake information is deleted.

### Claim
- The `claim` function allows users to claim their rewards. It verifies that the user has an active stake and that the claim interval has passed. Rewards are calculated based on the user's staked balance, the reward rate, and the current price obtained from the Chainlink oracle. The rewards are added to the user's reward balance, and the claim timestamp is updated. If it is the user's first reward, their address is added to the `rewardRecipients` array.

### Withdraw Reward
- The `withdrawReward` function allows users to withdraw their accumulated rewards. It transfers the reward amount from the contract to the user's address and resets the user's reward balance.

### Get Price
- The `getPrice` function retrieves the latest price from the Chainlink oracle by calling the `latestRoundData` function. It returns the price as a uint256 value.

### Get Reward Recipients
- The `getRewardRecipients` function returns an array of addresses representing users who have received rewards.

## Usage
1. Make sure you have the required dependencies and a Solidity compiler installed.
2. Import the Chainlink's AggregatorV3Interface contract.
3. Deploy the StakingContract contract by providing the `token` and `oracle` addresses.
4. Users can stake tokens by calling the `stake` function with the desired amount.
5.

 Users can claim their rewards using the `claim` function.
6. Users can withdraw their accumulated rewards via the `withdrawReward` function.
7. Users can unstake their staked tokens using the `unstake` function.
8. Utilize the available getter functions to retrieve specific information about stakes and reward recipients.

## Note
- Ensure that you have the necessary tokens to stake and interact with the contract.
- Adjust the minimum stake, reward rate, and claim interval constants according to your desired configuration.
