# Grants
Autonomous grant payment application


# Stake and pay contract with Chainlink API

1/ This contract allows a user to stake a certain amount of tokens (specified by minimumStake), and then automatically pays out a certain amount of tokens (specified by rewardRate) based on the price data obtained from the specified oracle API endpoint (oracle). 

2/ The contract uses the Chainlink AggregatorV3Interface to obtain the price data.

3/ The stake function allows a user to stake their tokens, and the unstake function allows them to unstake them. The claim function allows the user to claim their rewards based on the elapsed time since the last claim and the current price data obtained from the oracle API endpoint.

4/ The contract stores the staked balances of each user in the balances mapping, and the timestamp of their last claim in the lastClaimed mapping. It also stores whether or not a user has staked in.  It keeps track of stake and reward balances separately for each user using the Stake struct and the stakes mapping. When a user claims their rewards.

# Stake and pay contract with Etherscan API

1/ To use the Etherscan API to retrieve ERC-20 transaction data, we make a HTTP request to the API endpoint with the appropriate parameters.
