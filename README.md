# NFT Deposits Collection

NFT Deposits Collection - is an extension of [NFT Standard](https://github.com/ton-blockchain/TIPs/issues/62) that implements all the operations and get-methods of the original standard but adds some functionality that allow users to get an NFT on deposit of funds and get a reward for staking the deposit on change of the NFT after 180 days.

Prerequisites:

- lite-client
- FunC
- FIFT
- toncli

Smart-contracts

nft-collection.fc
nft-item.fc

Interesting files:

constants.fc

## FUNCTIONS

### Getting started

#### Prerequisites

- lite-client
- FunC
- FIFT
- toncli

#### build the project

`toncli build`

#### deploy the collection

`toncli deploy nft_collection`

### Methods for users

#### Deploy the deposit NFT

`toncli send --amount 5 --net testnet --address kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT --body /home/some_wallet/dev/projects/nft_stakable_collection/fift/deposit.fif`

#### Claim the reward

`toncli send --amount 0.02 --net testnet --address EQCGKv9J9C5vI2AyyZ9XpcSRHynWjUH-XOJNoNfJiMb5WULs --body /home/some_wallet/dev/projects/nft_stakable_collection/fift/claim_reward.fif`

### Collection owner methods

#### Deploy a new NFT
#### Batch deploy of new nfts
#### Change collection's owner
#### Change collection's content

### Get-methods

#### Get deposit data by the index of NFT

`toncli get --address kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT get_deposit_data_by_nft_index 0`

#### Get the dictionary with deposit NFT data

`toncli get --address kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT get_staking_contracts_dict`

#### Get all smart-contract's data

`toncli get --address kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT get_everything`

#### Get collection data
#### Get NFT address by index
#### Get royalty params
#### Get nft content

### Private Key Methods

#### Initiate stacking (coming soon)
#### Withdraw funds (coming soon)
#### Terminate stacking (coming soon)

## NFT Standart description

This project allows you to:

1.  Build basic nft collection contract
2.  Aims to *hopefully* test any nft collection contract for compliance with [NFT Standard](https://github.com/ton-blockchain/TIPs/issues/62)
3.  Deploy collection contract via `toncli deploy nft_collection`
4.  Manually deploy NFT item to the collection look (Deploying individual items)

#### Building

  Just run `toncli build`
  Depending on your fift/func build you may want
  to uncomment some *func/helpers*

#### Testing

  Build project and then: `toncli run_test`  

  ⚠ If you see `6` error code on all tests - you need to update your binary [more information here](https://github.com/disintar/toncli/issues/72)
  
#### Deploying collection contract

  This project consists of two subprojects **nft_item** and **nft_collection**
  You can see that in the *project.yml*
  **BOTH** of those have to be built.
  However, it makes sense to deploy only *nft_collection*.  
  Prior to deployment you need to check out *fift/collection-data.fif*
  and change all mock configuration values like collection_content,
  owner_address Etc.  
  To deploy run:`toncli deploy -n testnet nft_collection`.  
  
#### Deploying individual items

  To deploy your own NFT item to the already deployed collection
  you will need:  
  
+   Configure *fift/deploy.fif* script with your own values:
[Take a look](https://github.com/ton-blockchain/TIPs/issues/64)  

+   Make yourself familiar with process of sending  [internal messages](https://github.com/disintar/toncli/blob/master/docs/advanced/send_fift_internal.md)  

`toncli send -n testnet -a 0.05 -c nft_collection --body fift/deploy.fif`  
Every next item deployment you should make sure to
change item index in the *fift/deploy.fif* file ( Yes. Manually for now ).

#### Parse nft content

Parse nft for collection (will work only if collection-data is same with on-chain):

`toncli get get_nft_data -a "NFT_ADDRESS" --fift ./fift/parse-data-nft-collection.fif`

Parse nft for single:

`toncli get get_nft_data -a "NFT_ADDRESS" --fift ./fift/parse-data-nft-single.fif`
