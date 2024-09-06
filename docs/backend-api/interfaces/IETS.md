# IETS

This is the interface for the ETS.sol core contract that records ETS TaggingRecords to the blockchain.

## Functions

### createTaggingRecord

```solidity
function createTaggingRecord(uint256[] _tagIds, uint256 _targetId, string _recordType, address _tagger) external payable
```

Create a new tagging record.

Requirements:

- Caller must be relayer contract.
- CTAG(s) and TargetId must exist.

| Name         | Type      | Description                                                |
| ------------ | --------- | ---------------------------------------------------------- |
| \_tagIds     | uint256[] | Array of CTAG token Ids.                                   |
| \_targetId   | uint256   | targetId of the URI being tagged. See ETSTarget.sol        |
| \_recordType | string    | Arbitrary identifier for type of tagging record.           |
| \_tagger     | address   | Address calling Relayer contract to create tagging record. |

### getOrCreateTagId

```solidity
function getOrCreateTagId(string _tag, address payable _creator) external payable returns (uint256 tokenId)
```

Get or create CTAG token from tag string.

Combo function that accepts a tag string and returns corresponding CTAG token Id if it exists,
or if it doesn't exist, creates a new CTAG and then returns corresponding Id.

Only ETS Relayer contracts may call this function.

| Name      | Type            | Description                          |
| --------- | --------------- | ------------------------------------ |
| \_tag     | string          | Tag string.                          |
| \_creator | address payable | Address credited with creating CTAG. |

| Name    | Type    | Description       |
| ------- | ------- | ----------------- |
| tokenId | uint256 | Id of CTAG token. |

### createTag

```solidity
function createTag(string _tag, address payable _creator) external payable returns (uint256 tokenId)
```

Create CTAG token from tag string.

Reverts if tag exists or is invalid.

Only ETS Relayer contracts may call this function.

| Name      | Type            | Description                          |
| --------- | --------------- | ------------------------------------ |
| \_tag     | string          | Tag string.                          |
| \_creator | address payable | Address credited with creating CTAG. |

| Name    | Type    | Description       |
| ------- | ------- | ----------------- |
| tokenId | uint256 | Id of CTAG token. |

### applyTagsWithRawInput

```solidity
function applyTagsWithRawInput(struct IETS.TaggingRecordRawInput _rawInput, address payable _tagger) external payable
```

Apply one or more tags to a targetURI using tagging record raw client input data.

Like it's sister function applyTagsWithCompositeKey, records new ETS Tagging Record or appends tags to an
existing record if found to already exist. This function differs in that it creates new ETS target records
and CTAG tokens for novel targetURIs and hastag strings respectively. This function can only be called by
Relayer contracts.

| Name       | Type                              | Description                                                   |
| ---------- | --------------------------------- | ------------------------------------------------------------- |
| \_rawInput | struct IETS.TaggingRecordRawInput | Raw client input data formed as TaggingRecordRawInput struct. |
| \_tagger   | address payable                   | Address that calls Relayer to tag a targetURI.                |

### applyTagsWithCompositeKey

```solidity
function applyTagsWithCompositeKey(uint256[] _tagIds, uint256 _targetId, string _recordType, address payable _tagger) external payable
```

Apply one or more tags to a targetId using using tagging record composite key.

Records new ETS Tagging Record to the blockchain or appends tags if Tagging Record already exists. CTAGs and
targetId are created if they don't exist. Caller must be Relayer contract.

| Name         | Type            | Description                                             |
| ------------ | --------------- | ------------------------------------------------------- |
| \_tagIds     | uint256[]       | Array of CTAG token Ids.                                |
| \_targetId   | uint256         | targetId of the URI being tagged. See ETSTarget.sol     |
| \_recordType | string          | Arbitrary identifier for type of tagging record.        |
| \_tagger     | address payable | Address of that calls Relayer to create tagging record. |

### replaceTagsWithRawInput

```solidity
function replaceTagsWithRawInput(struct IETS.TaggingRecordRawInput _rawInput, address payable _tagger) external payable
```

Replace entire tag set in tagging record using raw data for record lookup.

If supplied tag strings don't have CTAGs, new ones are minted.

| Name       | Type                              | Description                                                   |
| ---------- | --------------------------------- | ------------------------------------------------------------- |
| \_rawInput | struct IETS.TaggingRecordRawInput | Raw client input data formed as TaggingRecordRawInput struct. |
| \_tagger   | address payable                   | Address that calls Relayer to tag a targetURI.                |

### replaceTagsWithCompositeKey

```solidity
function replaceTagsWithCompositeKey(uint256[] _tagIds, uint256 _targetId, string _recordType, address payable _tagger) external payable
```

Replace entire tag set in tagging record using composite key for record lookup.

This function overwrites the tags in a tagging record with the supplied tags, only
charging for the new tags in the replacement set.

| Name         | Type            | Description                                             |
| ------------ | --------------- | ------------------------------------------------------- |
| \_tagIds     | uint256[]       | Array of CTAG token Ids.                                |
| \_targetId   | uint256         | targetId of the URI being tagged. See ETSTarget.sol     |
| \_recordType | string          | Arbitrary identifier for type of tagging record.        |
| \_tagger     | address payable | Address of that calls Relayer to create tagging record. |

### removeTagsWithRawInput

```solidity
function removeTagsWithRawInput(struct IETS.TaggingRecordRawInput _rawInput, address _tagger) external
```

Remove one or more tags from a tagging record using raw data for record lookup.

| Name       | Type                              | Description                                                   |
| ---------- | --------------------------------- | ------------------------------------------------------------- |
| \_rawInput | struct IETS.TaggingRecordRawInput | Raw client input data formed as TaggingRecordRawInput struct. |
| \_tagger   | address                           | Address that calls Relayer to tag a targetURI.                |

### removeTagsWithCompositeKey

```solidity
function removeTagsWithCompositeKey(uint256[] _tagIds, uint256 _targetId, string _recordType, address payable _tagger) external
```

Remove one or more tags from a tagging record using composite key for record lookup.

| Name         | Type            | Description                                             |
| ------------ | --------------- | ------------------------------------------------------- |
| \_tagIds     | uint256[]       | Array of CTAG token Ids.                                |
| \_targetId   | uint256         | targetId of the URI being tagged. See ETSTarget.sol     |
| \_recordType | string          | Arbitrary identifier for type of tagging record.        |
| \_tagger     | address payable | Address of that calls Relayer to create tagging record. |

### appendTags

```solidity
function appendTags(uint256 _taggingRecordId, uint256[] _tagIds) external payable
```

Append one or more tags to a tagging record.

| Name              | Type      | Description                   |
| ----------------- | --------- | ----------------------------- |
| \_taggingRecordId | uint256   | tagging record being updated. |
| \_tagIds          | uint256[] | Array of CTAG token Ids.      |

### replaceTags

```solidity
function replaceTags(uint256 _taggingRecordId, uint256[] _tagIds) external payable
```

Replaces tags in tagging record.

This function overwrites the tags in a tagging record with the supplied tags, only
charging for the new tags in the replacement set.

| Name              | Type      | Description                   |
| ----------------- | --------- | ----------------------------- |
| \_taggingRecordId | uint256   | tagging record being updated. |
| \_tagIds          | uint256[] | Array of CTAG token Ids.      |

### removeTags

```solidity
function removeTags(uint256 _taggingRecordId, uint256[] _tagIds) external
```

Remove one or more tags from a tagging record.

| Name              | Type      | Description                   |
| ----------------- | --------- | ----------------------------- |
| \_taggingRecordId | uint256   | tagging record being updated. |
| \_tagIds          | uint256[] | Array of CTAG token Ids.      |

### drawDown

```solidity
function drawDown(address payable _account) external
```

Function for withdrawing funds from an accrual account. Can be called by the account owner
or on behalf of the account. Does nothing when there is nothing due to the account.

| Name      | Type            | Description                                                           |
| --------- | --------------- | --------------------------------------------------------------------- |
| \_account | address payable | Address of account being drawn down and which will receive the funds. |

### computeTaggingRecordIdFromRawInput

```solidity
function computeTaggingRecordIdFromRawInput(struct IETS.TaggingRecordRawInput _rawInput, address _relayer, address _tagger) external view returns (uint256 taggingRecordId)
```

Compute a taggingRecordId from raw input.

| Name       | Type                              | Description                                                   |
| ---------- | --------------------------------- | ------------------------------------------------------------- |
| \_rawInput | struct IETS.TaggingRecordRawInput | Raw client input data formed as TaggingRecordRawInput struct. |
| \_relayer  | address                           | Address of tagging record Relayer contract.                   |
| \_tagger   | address                           | Address interacting with Relayer to tag content ("Tagger").   |

| Name            | Type    | Description                             |
| --------------- | ------- | --------------------------------------- |
| taggingRecordId | uint256 | Unique identifier for a tagging record. |

### computeTaggingRecordIdFromCompositeKey

```solidity
function computeTaggingRecordIdFromCompositeKey(uint256 _targetId, string _recordType, address _relayer, address _tagger) external pure returns (uint256 taggingRecordId)
```

Compute & return a taggingRecordId.

Every TaggingRecord in ETS is mapped to by it's taggingRecordId. This Id is a composite key
composed of targetId, recordType, relayer contract address and tagger address hashed and cast as a uint256.

| Name         | Type    | Description                                                 |
| ------------ | ------- | ----------------------------------------------------------- |
| \_targetId   | uint256 | Id of target being tagged (see ETSTarget.sol).              |
| \_recordType | string  | Arbitrary identifier for type of tagging record.            |
| \_relayer    | address | Address of tagging record Relayer contract.                 |
| \_tagger     | address | Address interacting with Relayer to tag content ("Tagger"). |

| Name            | Type    | Description                             |
| --------------- | ------- | --------------------------------------- |
| taggingRecordId | uint256 | Unique identifier for a tagging record. |

### computeTaggingFeeFromRawInput

```solidity
function computeTaggingFeeFromRawInput(struct IETS.TaggingRecordRawInput _rawInput, address _relayer, address _tagger, enum IETS.TaggingAction _action) external view returns (uint256 fee, uint256 tagCount)
```

Compute tagging fee for raw input and desired action.

| Name       | Type                              | Description                                                                  |
| ---------- | --------------------------------- | ---------------------------------------------------------------------------- |
| \_rawInput | struct IETS.TaggingRecordRawInput | Raw client input data formed as TaggingRecordRawInput struct.                |
| \_relayer  | address                           | Address of tagging record Relayer contract.                                  |
| \_tagger   | address                           | Address interacting with Relayer to tag content ("Tagger").                  |
| \_action   | enum IETS.TaggingAction           | Integer representing action to be performed according to enum TaggingAction. |

| Name     | Type    | Description                                       |
| -------- | ------- | ------------------------------------------------- |
| fee      | uint256 | Calculated tagging fee in ETH/Matic               |
| tagCount | uint256 | Number of new tags being added to tagging record. |

### computeTaggingFeeFromCompositeKey

```solidity
function computeTaggingFeeFromCompositeKey(uint256[] _tagIds, uint256 _targetId, string _recordType, address _relayer, address _tagger, enum IETS.TaggingAction _action) external view returns (uint256 fee, uint256 tagCount)
```

Compute tagging fee for CTAGs, tagging record composite key and desired action.

| Name         | Type                    | Description                                                                  |
| ------------ | ----------------------- | ---------------------------------------------------------------------------- |
| \_tagIds     | uint256[]               | Array of CTAG token Ids.                                                     |
| \_targetId   | uint256                 |                                                                              |
| \_recordType | string                  |                                                                              |
| \_relayer    | address                 | Address of tagging record Relayer contract.                                  |
| \_tagger     | address                 | Address interacting with Relayer to tag content ("Tagger").                  |
| \_action     | enum IETS.TaggingAction | Integer representing action to be performed according to enum TaggingAction. |

| Name     | Type    | Description                                       |
| -------- | ------- | ------------------------------------------------- |
| fee      | uint256 | Calculated tagging fee in ETH/Matic               |
| tagCount | uint256 | Number of new tags being added to tagging record. |

### computeTaggingFee

```solidity
function computeTaggingFee(uint256 _taggingRecordId, uint256[] _tagIds, enum IETS.TaggingAction _action) external view returns (uint256 fee, uint256 tagCount)
```

Compute tagging fee for CTAGs, tagging record id and desired action.

If the global, service wide tagging fee is set (see ETS.taggingFee() & ETS.setTaggingFee()) ETS charges a per tag for all
new tags applied to a tagging record. This applies to both new tagging records and modified tagging records.

Computing the tagging fee involves checking to see if a tagging record exists and if so, given the desired action
(append or replace) determining the number of new tags being added and multiplying by the ETS per tag fee.

| Name              | Type                    | Description                                                                  |
| ----------------- | ----------------------- | ---------------------------------------------------------------------------- |
| \_taggingRecordId | uint256                 | Id of tagging record.                                                        |
| \_tagIds          | uint256[]               | Array of CTAG token Ids.                                                     |
| \_action          | enum IETS.TaggingAction | Integer representing action to be performed according to enum TaggingAction. |

| Name     | Type    | Description                                       |
| -------- | ------- | ------------------------------------------------- |
| fee      | uint256 | Calculated tagging fee in ETH/Matic               |
| tagCount | uint256 | Number of new tags being added to tagging record. |

### getTaggingRecordFromRawInput

```solidity
function getTaggingRecordFromRawInput(struct IETS.TaggingRecordRawInput _rawInput, address _relayer, address _tagger) external view returns (uint256[] tagIds, uint256 targetId, string recordType, address relayer, address tagger)
```

Retrieve a tagging record from it's raw input.

| Name       | Type                              | Description                                                   |
| ---------- | --------------------------------- | ------------------------------------------------------------- |
| \_rawInput | struct IETS.TaggingRecordRawInput | Raw client input data formed as TaggingRecordRawInput struct. |
| \_relayer  | address                           | Address of tagging record Relayer contract.                   |
| \_tagger   | address                           | Address interacting with Relayer to tag content ("Tagger").   |

| Name       | Type      | Description                                                 |
| ---------- | --------- | ----------------------------------------------------------- |
| tagIds     | uint256[] | CTAG token ids.                                             |
| targetId   | uint256   | TargetId that was tagged.                                   |
| recordType | string    | Type of tagging record.                                     |
| relayer    | address   | Address of tagging record Relayer contract.                 |
| tagger     | address   | Address interacting with Relayer to tag content ("Tagger"). |

### getTaggingRecordFromCompositeKey

```solidity
function getTaggingRecordFromCompositeKey(uint256 _targetId, string _recordType, address _relayer, address _tagger) external view returns (uint256[] tagIds, uint256 targetId, string recordType, address relayer, address tagger)
```

Retrieve a tagging record from composite key parts.

| Name         | Type    | Description                                                  |
| ------------ | ------- | ------------------------------------------------------------ |
| \_targetId   | uint256 | Id of target being tagged.                                   |
| \_recordType | string  | Arbitrary identifier for type of tagging record.             |
| \_relayer    | address | Address of Relayer contract that wrote tagging record.       |
| \_tagger     | address | Address of wallet that initiated tagging record via relayer. |

| Name       | Type      | Description                                                 |
| ---------- | --------- | ----------------------------------------------------------- |
| tagIds     | uint256[] | CTAG token ids.                                             |
| targetId   | uint256   | TargetId that was tagged.                                   |
| recordType | string    | Type of tagging record.                                     |
| relayer    | address   | Address of tagging record Relayer contract.                 |
| tagger     | address   | Address interacting with Relayer to tag content ("Tagger"). |

### getTaggingRecordFromId

```solidity
function getTaggingRecordFromId(uint256 _id) external view returns (uint256[] tagIds, uint256 targetId, string recordType, address relayer, address tagger)
```

Retrieve a tagging record from Id.

| Name | Type    | Description      |
| ---- | ------- | ---------------- |
| \_id | uint256 | taggingRecordId. |

| Name       | Type      | Description                                                 |
| ---------- | --------- | ----------------------------------------------------------- |
| tagIds     | uint256[] | CTAG token ids.                                             |
| targetId   | uint256   | TargetId that was tagged.                                   |
| recordType | string    | Type of tagging record.                                     |
| relayer    | address   | Address of tagging record Relayer contract.                 |
| tagger     | address   | Address interacting with Relayer to tag content ("Tagger"). |

### taggingRecordExistsByRawInput

```solidity
function taggingRecordExistsByRawInput(struct IETS.TaggingRecordRawInput _rawInput, address _relayer, address _tagger) external view returns (bool)
```

Check that a tagging record exists for given raw input.

| Name       | Type                              | Description                                                   |
| ---------- | --------------------------------- | ------------------------------------------------------------- |
| \_rawInput | struct IETS.TaggingRecordRawInput | Raw client input data formed as TaggingRecordRawInput struct. |
| \_relayer  | address                           | Address of tagging record Relayer contract.                   |
| \_tagger   | address                           | Address interacting with Relayer to tag content ("Tagger").   |

| Name | Type | Description                              |
| ---- | ---- | ---------------------------------------- |
| [0]  | bool | boolean; true for exists, false for not. |

### taggingRecordExistsByCompositeKey

```solidity
function taggingRecordExistsByCompositeKey(uint256 _targetId, string _recordType, address _relayer, address _tagger) external view returns (bool)
```

Check that a tagging record exists by it's componsite key parts.

| Name         | Type    | Description                                                  |
| ------------ | ------- | ------------------------------------------------------------ |
| \_targetId   | uint256 | Id of target being tagged.                                   |
| \_recordType | string  | Arbitrary identifier for type of tagging record.             |
| \_relayer    | address | Address of Relayer contract that wrote tagging record.       |
| \_tagger     | address | Address of wallet that initiated tagging record via relayer. |

| Name | Type | Description                              |
| ---- | ---- | ---------------------------------------- |
| [0]  | bool | boolean; true for exists, false for not. |

### taggingRecordExists

```solidity
function taggingRecordExists(uint256 _taggingRecordId) external view returns (bool)
```

Check that a tagging record exsits by it's Id.

| Name              | Type    | Description      |
| ----------------- | ------- | ---------------- |
| \_taggingRecordId | uint256 | taggingRecordId. |

| Name | Type | Description                              |
| ---- | ---- | ---------------------------------------- |
| [0]  | bool | boolean; true for exists, false for not. |

### totalDue

```solidity
function totalDue(address _account) external view returns (uint256 _due)
```

Function to check how much MATIC has been accrued by an address factoring in amount paid out.

| Name      | Type    | Description                           |
| --------- | ------- | ------------------------------------- |
| \_account | address | Address of the account being queried. |

| Name  | Type    | Description                            |
| ----- | ------- | -------------------------------------- |
| \_due | uint256 | Amount of WEI in MATIC due to account. |

### taggingFee

```solidity
function taggingFee() external view returns (uint256)
```

Function to retrieve the ETS platform tagging fee.

| Name | Type    | Description  |
| ---- | ------- | ------------ |
| [0]  | uint256 | tagging fee. |

## Events

### AccessControlsSet

```solidity
event AccessControlsSet(address newAccessControls)
```

_emitted when the ETS Access Controls is set._

| Name              | Type    | Description                                 |
| ----------------- | ------- | ------------------------------------------- |
| newAccessControls | address | contract address access controls is set to. |

### TaggingFeeSet

```solidity
event TaggingFeeSet(uint256 newTaggingFee)
```

_emitted when ETS tagging fee is set._

| Name          | Type    | Description      |
| ------------- | ------- | ---------------- |
| newTaggingFee | uint256 | new tagging fee. |

### PercentagesSet

```solidity
event PercentagesSet(uint256 platformPercentage, uint256 relayerPercentage)
```

_emitted when participant distribution percentages are set._

| Name               | Type    | Description                                                                                     |
| ------------------ | ------- | ----------------------------------------------------------------------------------------------- |
| platformPercentage | uint256 | percentage of tagging fee allocated to ETS.                                                     |
| relayerPercentage  | uint256 | percentage of tagging fee allocated to relayer of record for CTAG being used in tagging record. |

### TaggingRecordCreated

```solidity
event TaggingRecordCreated(uint256 taggingRecordId)
```

_emitted when a new tagging record is recorded within ETS._

| Name            | Type    | Description                          |
| --------------- | ------- | ------------------------------------ |
| taggingRecordId | uint256 | Unique identifier of tagging record. |

### TaggingRecordUpdated

```solidity
event TaggingRecordUpdated(uint256 taggingRecordId, enum IETS.TaggingAction action)
```

_emitted when a tagging record is updated._

| Name            | Type                    | Description                                   |
| --------------- | ----------------------- | --------------------------------------------- |
| taggingRecordId | uint256                 | tagging record being updated.                 |
| action          | enum IETS.TaggingAction | Type of update applied as TaggingAction enum. |

### FundsWithdrawn

```solidity
event FundsWithdrawn(address who, uint256 amount)
```

_emitted when ETS participant draws down funds accrued to their contract or wallet._

| Name   | Type    | Description                                  |
| ------ | ------- | -------------------------------------------- |
| who    | address | contract or wallet address being drawn down. |
| amount | uint256 | amount being drawn down.                     |
