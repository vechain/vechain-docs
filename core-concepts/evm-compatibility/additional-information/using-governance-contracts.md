# Using Governance Contracts

This page documents the various governance contracts and their tests that can be found in the [governance examples](https://github.com/vechainfoundation/governance-examples) repository.

## GovernorTimelockCompound

`GovernorTimelockCompound.sol` is an abstract smart contract that is provided by the Openzeppelin project and it belongs to the Governance category of contracts. In general, governance contracts are used to control on chain-governance (i.e. decision making). `GovernorTimelockCompound.sol` is also a `Governor.sol` contract which means that it inherits all the logic and primitives for on chain governance. In addition to that `GovernorTimelockCompound.sol` also binds the execution of a proposal to a Compound Timelock which means that any proposal will have a time delay enforced by the `TimelockController.sol` contract. Since `GovernorTimelockCompound.sol` is abstract, to use it one would have to create a new so called mock contract that inherits from it and implement the necessary functionality for their use-case.

### Example Use-case

A common use-case for on-chain governance contracts is voting for a proposal. This could be used in DAOs where stakeholders have the ability to vote on a proposal that will execute if a threshold of participants agree with its execution. A proposal is just a sequence of actions and it consists of target addresses, calldata which encodes a function call and an amount of VET to include. Essentially it is a collection of transactions that can either transfer value or call a function in any contract. In order to create a proposal an Admin(?) of the Governor contract can call the `propose` function and pass the target addresses, value and data as well as a proposal description. Then the stakeholders of the DAO can cast a vote using the `castVote` function. In our case `GovernorTimelockCompound.sol` will delegate the proposal activation to `TimelockCompound.sol` which will impose a time delay between proposal activation and it actually taking effect, giving time to users to react to the change before it takes effect.

### Changes

In order to make some tests provided by Openzeppelin work with the various governance contracts some changes had to be made. For example a new function was added to [CompTimelock.sol](https://github.com/vechainfoundation/openzeppelin-tests/commit/1f9acb7628c7f4ba14efbbe195e3d483159d8f04#diff-568461a21df5aa294f510532fbc53aaf531d74d734e27a15fc5baada38418819) where one can change the admin of the contract externally after its construction. In the corresponding test in [GovernorTimelockCompound.test.js](https://github.com/vechainfoundation/openzeppelin-tests/commit/1f9acb7628c7f4ba14efbbe195e3d483159d8f04#diff-2793b79dcc646a0832dccdcbb19c7e599106d97d274c0d763e69594065aafffd) the admin value of the timelock contract is set to the address of the `Governor` instance that is also deployed in the same test case. Originally in the test there is a function that can predicts the Governor's contract address and passes it as a value in the Timelock contract's constructor before the Governor is deployed. But since there are differences between Ethereum and VeChain, the same contract prediction does not work for VeChain contracts. Thus, why we had to manually set the admin value.

### How to use

In order to use `GovernorTimelockCompound.sol` for your own project the following steps are required:

#### Import the required contracts

```solidity
import "@openzeppelin/contracts/governance/extensions/GovernorTimelockCompound.sol";
import "@openzeppelin/contracts/governance/extensions/GovernorSettings.sol";
import "@openzeppelin/contracts/governance/extensions/GovernorCountingSimple.sol";
import "@openzeppelin/contracts/governance/extensions/GovernorVotesQuorumFraction.sol";
```

#### Create a mock contract

Create a new contract that inherits from `GovernorTimelockCompound.sol` in order to inherit its functionality.

```solidity
contract GovernorTimelockCompoundMock is GovernorTimelockCompound {
    // ...
}
```

While the core logic is given by the Governor contract we also need to inherrit some other helper contracts to control different parameters. For example we will also need to inherit the `GovernorSettings.sol` in order to manage some of the governance settings such as voting delay, voting period duration and proposal threshold), `GovernorVotesQuorumFraction.sol` in order to determine how many votes are needed for quorum, `GovernorCountingSimple.sol` in order to provide users with options with regards to voting (e.g. For, Against and Abstain) and of course `GovernorTimelockCompound.sol` for the main functionality which is connecting the governor contract with an instance of a compound timelock contract. Taking everything into consideration the updated constructor looks like this:

```solidity
contract GovernorTimelockCompoundMock is
    GovernorSettings,
    GovernorTimelockCompound,
    GovernorVotesQuorumFraction,
    GovernorCountingSimple
{
    constructor(
        string memory name_,
        IVotes token_,
        uint256 votingDelay_,
        uint256 votingPeriod_,
        ICompoundTimelock timelock_,
        uint256 quorumNumerator_
    )
        Governor(name_)
        GovernorTimelockCompound(timelock_)
        GovernorSettings(votingDelay_, votingPeriod_, 0)
        GovernorVotes(token_)
        GovernorVotesQuorumFraction(quorumNumerator_)
    {}
```

Notice that we also need to call the `Governor` and `GovernorVotes` constructors even though we have not directly inherited from these contracts. The reason is that other contracts that we are using inherit from them. For example `GovernorVotesQuorumFraction.sol` inherits from `GovernorVotes.sol` thus we need to also call its constructor if we want to customize the functionality. Finally note that in order to be able to deploy the mock contract we also need to have a deployed version of `CompoundTimelock` since its address is required as an input parameter to the `GovernorTimelockCompound` constructor.

#### Implement Necessary Functions

After we have inherited from `GovernorTimelockCompound.sol` and helper contracts we need to override some of its functions because they are implemented by multiple contracts. This creates a problem because there are two or more base classes that define a function with the same name and parameter types, and our derived contract is trying to inherit from them. This creates an ambiguity for the derived contract, as it is not clear which version of the function to use. The derived contract in this case is of course our `GovernorTimelockCompoundMock.sol` contract. We will use the override keyword in Solidity to define the concrete functionality in order to remove ambiguity and be able to compile our contracts and/or define new functionality. The following functions will be overridden:

* `supportsInterface` returns a boolean value representing whether the contract supports a given interface
* `quorum` returns the number of votes a proposal has
* `state` returns the state of a proposal
* `proposalThreshold` returns the number of votes required in order for a voter to become a proposer
* `_execute` executes a proposal
* `_cancel` cancels proposal
* `_executor` returns the address of the proposal's executor

The complete mock contract can be found below

```solidity
contract GovernorTimelockCompoundMock is
    GovernorSettings,
    GovernorTimelockCompound,
    GovernorVotesQuorumFraction,
    GovernorCountingSimple
{
    constructor(
        string memory name_,
        IVotes token_,
        uint256 votingDelay_,
        uint256 votingPeriod_,
        ICompoundTimelock timelock_,
        uint256 quorumNumerator_
    )
        Governor(name_)
        GovernorTimelockCompound(timelock_)
        GovernorSettings(votingDelay_, votingPeriod_, 0)
        GovernorVotes(token_)
        GovernorVotesQuorumFraction(quorumNumerator_)
    {}

    function supportsInterface(
        bytes4 interfaceId
    ) public view override(Governor, GovernorTimelockCompound) returns (bool) {
        return super.supportsInterface(interfaceId);
    }

    function quorum(
        uint256 blockNumber
    ) public view override(IGovernor, GovernorVotesQuorumFraction) returns (uint256) {
        return super.quorum(blockNumber);
    }

    function cancel(
        address[] memory targets,
        uint256[] memory values,
        bytes[] memory calldatas,
        bytes32 salt
    ) public returns (uint256 proposalId) {
        return _cancel(targets, values, calldatas, salt);
    }

    /**
     * Overriding nightmare
     */
    function state(
        uint256 proposalId
    ) public view override(Governor, GovernorTimelockCompound) returns (ProposalState) {
        return super.state(proposalId);
    }

    function proposalThreshold() public view override(Governor, GovernorSettings) returns (uint256) {
        return super.proposalThreshold();
    }

    function _execute(
        uint256 proposalId,
        address[] memory targets,
        uint256[] memory values,
        bytes[] memory calldatas,
        bytes32 descriptionHash
    ) internal override(Governor, GovernorTimelockCompound) {
        super._execute(proposalId, targets, values, calldatas, descriptionHash);
    }

    function _cancel(
        address[] memory targets,
        uint256[] memory values,
        bytes[] memory calldatas,
        bytes32 salt
    ) internal override(Governor, GovernorTimelockCompound) returns (uint256 proposalId) {
        return super._cancel(targets, values, calldatas, salt);
    }

    function _executor() internal view override(Governor, GovernorTimelockCompound) returns (address) {
        return super._executor();
    }
}
```

Note that when a contract inherits from multiple other contracts that implement the same virtual function (e.g. `A`), and if that contract overrides the function by running `super.A()` then the function that runs will be the one that is last in the inheritance list. For example in the following example

```solidity
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;
contract Parent1 {
  function foo() public virtual pure returns (string memory) {
    return "Hello from Parent1";
  }
}

contract Parent2 {
  function foo() public virtual pure returns (string memory) {
    return "Hello from Parent2";
  }
}

contract Test is Parent2, Parent1 {
  function foo() public override(Parent1, Parent2) pure returns (string memory) {
    return super.foo();
  }
}

```

when running `super.foo()` in the Test contract it will execute the implementation found in Parent1 since its last in the inheritance list.

### Testing

In order to test the functionality and demonstrate potential use cases, one can create test cases where an owner of the mock contract creates a proposal and a number of voters vote on it. Depending on the votes the proposal can be executed at a future time or rejected. This is demonstrated in the tests included in the examples repository. To run the tests provided in the examples repository simply run:

```bash
npx hardhat test --network vechain test/sample/GovernorTimelockCompound.test.js
```

## GovernorTimelockControl

`GovernorTimelockControl.sol` is another abstract contract provided by the Openzeppelin project. It is very similar to the aforementioned `GovernorTimelockCompound.sol` contract in that its main purpose is to be used for on-chain governance. The main difference is the choice of time-lock between the two contracts. While `GovernorTimelockCompound.sol` uses the `TimelockCompound.sol` contract for time-lock purposes `GovernorTimelockControl.sol` uses a TimelockController instance.

### How to use

#### Import the required contracts

```solidity
import "@openzeppelin/contracts/governance/extensions/GovernorTimelockControl.sol";
import "@openzeppelin/contracts/governance/extensions/GovernorSettings.sol";
import "@openzeppelin/contracts/governance/extensions/GovernorCountingSimple.sol";
import "@openzeppelin/contracts/governance/extensions/GovernorVotesQuorumFraction.sol";
```

#### Implement necessary functions

Similarly to `GovernorTimelockCompound.sol` we need to implement the same functions in order to create the mock contract. The full contract can be found below:

```solidity
contract GovernorTimelockControlMock is
    GovernorSettings,
    GovernorTimelockControl,
    GovernorVotesQuorumFraction,
    GovernorCountingSimple
{
    constructor(
        string memory name_,
        IVotes token_,
        uint256 votingDelay_,
        uint256 votingPeriod_,
        TimelockController timelock_,
        uint256 quorumNumerator_
    )
        Governor(name_)
        GovernorTimelockControl(timelock_)
        GovernorSettings(votingDelay_, votingPeriod_, 0)
        GovernorVotes(token_)
        GovernorVotesQuorumFraction(quorumNumerator_)
    {}

    function supportsInterface(
        bytes4 interfaceId
    ) public view override(Governor, GovernorTimelockControl) returns (bool) {
        return super.supportsInterface(interfaceId);
    }

    function quorum(
        uint256 blockNumber
    ) public view override(IGovernor, GovernorVotesQuorumFraction) returns (uint256) {
        return super.quorum(blockNumber);
    }

    function cancel(
        address[] memory targets,
        uint256[] memory values,
        bytes[] memory calldatas,
        bytes32 descriptionHash
    ) public returns (uint256 proposalId) {
        return _cancel(targets, values, calldatas, descriptionHash);
    }

    /**
     * Overriding nightmare
     */
    function state(uint256 proposalId) public view override(Governor, GovernorTimelockControl) returns (ProposalState) {
        return super.state(proposalId);
    }

    function proposalThreshold() public view override(Governor, GovernorSettings) returns (uint256) {
        return super.proposalThreshold();
    }

    function _execute(
        uint256 proposalId,
        address[] memory targets,
        uint256[] memory values,
        bytes[] memory calldatas,
        bytes32 descriptionHash
    ) internal override(Governor, GovernorTimelockControl) {
        super._execute(proposalId, targets, values, calldatas, descriptionHash);
    }

    function _cancel(
        address[] memory targets,
        uint256[] memory values,
        bytes[] memory calldatas,
        bytes32 descriptionHash
    ) internal override(Governor, GovernorTimelockControl) returns (uint256 proposalId) {
        return super._cancel(targets, values, calldatas, descriptionHash);
    }

    function _executor() internal view override(Governor, GovernorTimelockControl) returns (address) {
        return super._executor();
    }

    function nonGovernanceFunction() external {}
}
```

### Testing

Finally, in order to test our newly created mock contract we need to run it with the following command

```bash
npx hardhat test --network vechain test/sample/GovernorTimelockControl.test.js
```
