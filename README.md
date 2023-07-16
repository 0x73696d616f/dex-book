# DexBook

## Frontend

The frontend is available at https://github.com/0x73696d616f/dex-book-frontend.

## Smart Contracts

The smart contracts are available at https://github.com/0x73696d616f/dex-book-contracts.

## Neural Network

The GRU neural network code can be found here https://github.com/0x73696d616f/dex-book-nn.

## Efficient Order Book Implementation

DexBook stores sell and buy orders in separate data structures, having a linked list of ordered prices and each node has a linked list of orders from different addresses.

This implementation would mean delete, update actions of O(1) time and insert of O(n), which is still expensive.

To overcome this, insertion hints are used, giving the previous and next prices of the to be inserted price, making it a O(1) insertion.

## GRU neural network

A gated recurrent unit neural network was training on Bitcoin/USD data of 2 years in tensorflow. It looks at the last 10 day average prices and predicts the price in 24 hours. The model shows promising results as can be seen [here](https://github.com/0x73696d616f/dex-book-nn).

## Storing the neural network

The GRU neural network is stored on the blockchain using [SSTORE2](https://github.com/transmissions11/solmate/blob/main/src/utils/SSTORE2.sol), which is much cheaper and scales better. A neural network of any size can be stored. Then, using tensorflowJs and the rpc url, it predicts the prices.