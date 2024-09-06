# ETSRelayer

Sample implementation of IETSRelayer

## Functions

### constructor

```solidity
constructor(contract IETS _ets, contract IETSToken _etsToken, contract IETSTarget _etsTarget, address payable _creator, address payable _owner) public
```

### pause

```solidity
function pause() public
```

Pause this relayer contract.

_This function can only be called by the owner when the contract is unpaused._

### unpause

```solidity
function unpause() public
```

Unpause this relayer contract.

_This function can only be called by the owner when the contract is paused._

### changeOwner

```solidity
function changeOwner(address _newOwner) public
```

Transfer this contract to a new owner.

_This function can only be called by the owner when the contract is paused._

| Name       | Type    | Description |
| ---------- | ------- | ----------- |
| \_newOwner | address |             |

### applyTags

```solidity
function applyTags(struct IETS.TaggingRecordRawInput[] _rawParts) public payable
```

### replaceTags

```solidity
function replaceTags(struct IETS.TaggingRecordRawInput[] _rawParts) public payable
```

### removeTags

```solidity
function removeTags(struct IETS.TaggingRecordRawInput[] _rawParts) public payable
```

### getOrCreateTagIds

```solidity
function getOrCreateTagIds(string[] _tags) public payable returns (uint256[] _tagIds)
```

### supportsInterface

```solidity
function supportsInterface(bytes4 interfaceId) public view virtual returns (bool)
```

_See {IERC165-supportsInterface}._

### isPausedByOwner

```solidity
function isPausedByOwner() public view virtual returns (bool)
```

Check whether this contract has been pasued by the owner.

_Pause functionality should be provided by OpenZeppelin Pausable utility._

| Name | Type | Description                                     |
| ---- | ---- | ----------------------------------------------- |
| [0]  | bool | boolean: true for paused; false for not paused. |

### getOwner

```solidity
function getOwner() public view virtual returns (address payable)
```

Returns address of an IETSRelayer contract owner.

| Name | Type            | Description                |
| ---- | --------------- | -------------------------- |
| [0]  | address payable | address of contract owner. |

### getRelayerName

```solidity
function getRelayerName() public pure returns (string)
```

Returns human readable name for this IETSRelayer contract.

| Name | Type   | Description                               |
| ---- | ------ | ----------------------------------------- |
| [0]  | string | name of the Relayer contract as a string. |

### getCreator

```solidity
function getCreator() public view returns (address payable)
```

Returns address of an IETSRelayer contract creator.

| Name | Type            | Description                                     |
| ---- | --------------- | ----------------------------------------------- |
| [0]  | address payable | address of the creator of the Relayer contract. |

### computeTaggingFee

```solidity
function computeTaggingFee(uint256 _taggingRecordId, uint256[] _tagIds, enum IETS.TaggingAction _action) public view returns (uint256 fee, uint256 tagCount)
```

### \_applyTags

```solidity
function _applyTags(struct IETS.TaggingRecordRawInput _rawParts, address payable _tagger, uint256 _taggingFee) internal
```

### \_replaceTags

```solidity
function _replaceTags(struct IETS.TaggingRecordRawInput _rawParts, address payable _tagger, uint256 _taggingFee) internal
```

### \_removeTags

```solidity
function _removeTags(struct IETS.TaggingRecordRawInput _rawParts, address payable _tagger) internal
```
