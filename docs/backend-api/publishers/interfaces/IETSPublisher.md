# IETSRelayer

Minimum interface required for ETS Relayer smart contracts. Contracts implementing this
interface will need to import OpenZeppelin ERC165, Ownable and Pausable contracts.
See https://github.com/ethereum-tag-service/ets/blob/stage/packages/contracts/contracts/examples/ETSRelayer.sol
for a sample implementation.

## Functions

### pause

```solidity
function pause() external
```

Pause this relayer contract.

_This function can only be called by the owner when the contract is unpaused._

### unpause

```solidity
function unpause() external
```

Unpause this relayer contract.

_This function can only be called by the owner when the contract is paused._

### changeOwner

```solidity
function changeOwner(address newOwner) external
```

Transfer this contract to a new owner.

_This function can only be called by the owner when the contract is paused._

| Name     | Type    | Description                        |
| -------- | ------- | ---------------------------------- |
| newOwner | address | Address of the new contract owner. |

### supportsInterface

```solidity
function supportsInterface(bytes4 interfaceId) external view returns (bool)
```

Broadcast support for IETSRelayer interface to external contracts.

_ETSCore will only add relayer contracts that implement IETSRelayer interface.
Your implementation should broadcast that it implements IETSRelayer interface._

| Name | Type | Description                                                                      |
| ---- | ---- | -------------------------------------------------------------------------------- |
| [0]  | bool | boolean: true if this contract implements the interface defined by `interfaceId` |

### isPausedByOwner

```solidity
function isPausedByOwner() external view returns (bool)
```

Check whether this contract has been pasued by the owner.

_Pause functionality should be provided by OpenZeppelin Pausable utility._

| Name | Type | Description                                     |
| ---- | ---- | ----------------------------------------------- |
| [0]  | bool | boolean: true for paused; false for not paused. |

### getOwner

```solidity
function getOwner() external view returns (address payable)
```

Returns address of an IETSRelayer contract owner.

| Name | Type            | Description                |
| ---- | --------------- | -------------------------- |
| [0]  | address payable | address of contract owner. |

### getRelayerName

```solidity
function getRelayerName() external view returns (string)
```

Returns human readable name for this IETSRelayer contract.

| Name | Type   | Description                               |
| ---- | ------ | ----------------------------------------- |
| [0]  | string | name of the Relayer contract as a string. |

### getCreator

```solidity
function getCreator() external view returns (address payable)
```

Returns address of an IETSRelayer contract creator.

| Name | Type            | Description                                     |
| ---- | --------------- | ----------------------------------------------- |
| [0]  | address payable | address of the creator of the Relayer contract. |

## Events

### RelayerPauseToggledByOwner

```solidity
event RelayerPauseToggledByOwner(address relayerAddress)
```

_Emitted when an IETSRelayer contract is paused/unpaused._

| Name           | Type    | Description                  |
| -------------- | ------- | ---------------------------- |
| relayerAddress | address | Address of relayer contract. |

### RelayerOwnerChanged

```solidity
event RelayerOwnerChanged(address relayerAddress)
```

_Emitted when an IETSRelayer contract has changed owners._

| Name           | Type    | Description                  |
| -------------- | ------- | ---------------------------- |
| relayerAddress | address | Address of relayer contract. |
