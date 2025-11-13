# Built-in Contracts

Examples of how to use the built-in contracts can be found [here](https://github.com/vechain/thor-builtins/tree/master/examples).

### authority.sol <a href="#authority-sol" id="authority-sol"></a>

[authority.sol ](https://github.com/vechain/thor/blob/master/builtin/gen/authority.sol)is related to the proof of authority (PoA) consensus mechanism. The Authority contract manages a list of candidate proposers that are responsible for packing transactions into a block. The proposers are authorized by a voting committee, but only the first 101 proposers in the candidates list can build a block. A candidate proposer includes signer address, endorsor address and identity. Signer address is related to sign a block, endorsor address is used for charging miner's fee and identity is used for identifying the proposer.

**Address** :0x0000000000000000000000417574686f72697479

[Code](https://github.com/vechain/thor/blob/master/builtin/gen/authority.sol) / [ABI](https://raw.githubusercontent.com/vechain/b32/master/ABIs/authority.json)

### energy.sol <a href="#energy-sol" id="energy-sol"></a>

[energy.sol ](https://github.com/vechain/thor/blob/master/builtin/gen/energy.sol)represents the sub-token in VechainThor which conforms to VIP-180(ERC-20) standard. The name of the token is VeThor and the symbol is VTHO. 1 VTHO equals to 1e18 Wei. The main function of VTHO is to pay for the transaction fee. VTHO is generated from VET, so the initial supply of VTHO is zero in the genesis block. The growth rate of VTHO is 5000000000 wei per token(VET) per second, that is to say 1 VET will produce about 0.000432 VTHO per day. The miner will be rewarded with 30 percent of transaction fee and the remaining 70 percent of the transaction fee will be burned. So the total supply of VTHO is dynamic.

**Address** :0x0000000000000000000000000000456e65726779

[Code ](https://github.com/vechain/thor/blob/master/builtin/gen/energy.sol)/ [ABI](https://raw.githubusercontent.com/vechain/b32/master/ABIs/energy.json)

### executor.sol <a href="#executor-sol" id="executor-sol"></a>

[executor.sol ](https://github.com/vechain/thor/blob/master/builtin/gen/executor.sol)represents the core code for the on-chain governance. The contract enables a proposal to be executed automatically on VechainThor if it is approved by at least two-thirda of the steering committee members. A proposal can be registered either by an approver (a steering committee member) or by an authorized voting contract.

**Address** : 0x0000000000000000000000004578656375746f72

[Code](https://github.com/vechain/thor/blob/master/builtin/gen/executor.sol) / [ABI](https://raw.githubusercontent.com/vechain/b32/master/ABIs/executor.json)

### extension-v2.sol <a href="#extension-v2-sol" id="extension-v2-sol"></a>

[extension-v2.sol ](https://github.com/vechain/thor/blob/master/builtin/gen/extension-v2.sol)extends EVM functions. It allows the developer to get information of the current transaction and any historical block within range of the genesis block to the best block. The information obtained based on block number includes blockID, blockTotalScore, blockTime and blockSigner. The developer can also get the current transaction information, including txGasPayer, txProvedWork, txID, txBlockRef and txExpiration.

> Note
>
> Before implement the VIP-191 , [extension.sol ](https://github.com/vechain/thor/blob/master/builtin/gen/extension.sol)is the main contract

**Address** : 0x0000000000000000000000457874656e73696f6e

[V1 Code](https://github.com/vechain/thor/blob/master/builtin/gen/extension.sol) / [V2 code ](https://github.com/vechain/thor/blob/master/builtin/gen/extension-v2.sol)/ [ABI](https://raw.githubusercontent.com/vechain/b32/master/ABIs/extension.json)

### params.sol <a href="#params-sol" id="params-sol"></a>

[params.sol ](https://github.com/vechain/thor/blob/master/builtin/gen/params.sol)stores the governance params of VechainThor. The params can be set by the executor, a contract that is authorized to modify governance params by a voting Committee. Anyone can get the params just by calling "get" function. The governance params is written in genesis block at launch time. You can find the list of the governance parameters in [params.go](https://github.com/vechain/thor/blob/master/thor/params.go).

**Address** : 0x0000000000000000000000000000506172616d73

[Code](https://github.com/vechain/thor/blob/master/builtin/gen/params.sol) / [ABI](https://raw.githubusercontent.com/vechain/b32/master/ABIs/params.json)

### prototype.sol <a href="#prototype-sol" id="prototype-sol"></a>

[prototype.sol ](https://github.com/vechain/thor/blob/master/builtin/gen/prototype.sol)is an account management model of VechainThor. In the account management model every contract has a master account, which, by default, is the creator of a contract. The master account plays the role of a contract manager, which has some authorities including "setMaster", "setCreditPlan", "addUser", "removeUser" and "selectSponsor". Every contract keeps a list of users who can call the contract for free but limited by credit. The user of a specific contract can be either added or removed by the contract master. Although from a user's perspective the fee is free, it is paid by a sponsor of the contract. Anyone can be a sponsor of a contract, just by calling sponsor function, and also the sponsor identity can be cancelled by calling unsponsor function. A contract may have more than one sponsor, but only the current sponsor chosen by master needs to pay the fee for the contract. If the current sponsor is out of energy, the master can select a sponsor from other sponsors candidates by calling selectSponsor function. The creditPlan can be set by the master which includes credit and recoveryRate. Every user has the same original credit. Every transaction consumes some amount of credit which is equal to the fee of the transaction, and the user can also pay the fee by itself if the gas payer is out of the credit. The credit can be recovered based on recoveryRate (per block).

**Address** : 0x000000000000000000000050726f746f74797065

[Code](https://github.com/vechain/thor/blob/master/builtin/gen/prototype.sol) / [ABI](https://raw.githubusercontent.com/vechain/b32/master/ABIs/prototype.json) / [Event ABI](https://raw.githubusercontent.com/vechain/b32/master/ABIs/prototype-event.json)
