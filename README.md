# NFT Deposits Collection

NFT Deposits Collection - is an extension of [NFT Standard](https://github.com/ton-blockchain/TIPs/issues/62) that implements all the operations and get-methods of the original standard but adds some functionality that allow users to get an NFT on deposit of funds and get a reward for staking the deposit on change of the NFT after 180 days.

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

#### Testing

`toncli run_test`

#### deploy the collection

This project consists of two subprojects **nft_item** and **nft_collection**
You can see that in the *project.yml*
**BOTH** of those have to be built.
However, it makes sense to deploy only *nft_collection*.  
Prior to deployment you need to check out *fift/collection-data.fif*
and change all mock configuration values like collection_content,
owner_address Etc.  
To deploy run:`toncli deploy -n testnet nft_collection`.  

### Methods for users

#### Deploy the deposit NFT

Users can send a transaction with funds and get-back an NFT of deposit, that acts as a provement for the reward.

`toncli send --amount 5 --net testnet --address kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT --body /home/some_wallet/dev/projects/nft_stakable_collection/fift/deposit.fif`

#### Claim the reward

User can send a message to his NFT for claiming reward. NFT will forward this message to the collection's contract. If message will pass all the verifications on the side of the collection's contract, the reward will be sent to the wallet, stipulated in the message.

`toncli send --amount 0.02 --net testnet --address EQCGKv9J9C5vI2AyyZ9XpcSRHynWjUH-XOJNoNfJiMb5WULs --body /home/some_wallet/dev/projects/nft_stakable_collection/fift/claim_reward.fif`

#### Claim reward partially

Coming soon

### Collection owner methods

#### Deploy a new NFT

To deploy your own NFT item to the already deployed collection you will need:

Configure *fift/deploy.fif* script with your own values:
[Take a look](https://github.com/ton-blockchain/TIPs/issues/64)  

Make yourself familiar with process of sending  [internal messages](https://github.com/disintar/toncli/blob/master/docs/advanced/send_fift_internal.md)  

`toncli send -n testnet -a 0.05 -c nft_collection --body fift/deploy.fif`  
Every next item deployment you should make sure to change item index in the *fift/deploy.fif* file ( Yes. Manually for now ).

#### Batch deploy of new nfts

Coming soon

#### Change collection's owner

Description soon

#### Change collection's content

Description soon

### Custom get-methods

#### Get deposit data by the index of NFT

You can pass the index of NFT to the get-method of collection's contract to get the reward unix-time of the deposit and the amount of the reward. This code is extendable and we can pass any additional information as a responce of this method.

`toncli get --address kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT get_deposit_data_by_nft_index 0`

#### Get the dictionary with deposit NFT data

You can get full dictionary stored in collection's contract with data about all deposits.

`toncli get --address kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT get_staking_contracts_dict`

#### Get all smart-contract's data

Running this method will return all the data, stored in the storage of the smart-contract: owner_address, next_item_index, content, nft_item_code, royalty_params, stored_seqno, public_key, min_deposit_amount, semi_annual_yield, staking_contracts_dict (dict with data about all deposits).

`toncli get --address kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT get_everything`

### Custom get-methods

Please note that as our contract comlies with the Standart of NFT, we implement all the standart methods. You can find their full description in [NFT Standard #62](https://github.com/ton-blockchain/TIPs/issues/62)

#### Get collection data

`toncli get --address kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT get_collection_data`

#### Get NFT address by index

`toncli get --address kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT get_nft_address_by_index`

#### Get royalty params

`toncli get --address kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT royalty_params`

#### Get nft content

`toncli get --address kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT get_nft_content`

### Parsing nft content

Parse nft for collection (will work only if collection-data is same with on-chain):

`toncli get get_nft_data -a kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT --fift ./fift/parse-data-nft-collection.fif`

Parse nft for single:

`toncli get get_nft_data -a kQDZeh9RCQmYwe29oQMdbocjqtFtnvBPWKF_BMFRxaVjF-vT --fift ./fift/parse-data-nft-single.fif`

### Private Key Methods

#### Initiate stacking

Coming soon

#### Withdraw funds (coming soon)

Coming soon

#### Terminate stacking (coming soon)

Coming soon