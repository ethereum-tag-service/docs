# IETSRelayerV1

Interface for the IETSRelayerV1 contract.

## Functions

### applyTags

```solidity
function applyTags(struct IETS.TaggingRecordRawInput[] _rawInput) external payable
```

Apply one or more tags to a targetURI using tagging record raw client input data.

| Name       | Type                                | Description                                                   |
| ---------- | ----------------------------------- | ------------------------------------------------------------- |
| \_rawInput | struct IETS.TaggingRecordRawInput[] | Raw client input data formed as TaggingRecordRawInput struct. |

### replaceTags

```solidity
function replaceTags(struct IETS.TaggingRecordRawInput[] _rawInput) external payable
```

Replace entire tag set in tagging record using raw data for record lookup.

If supplied tag strings don't have CTAGs, new ones are minted.

| Name       | Type                                | Description                                                   |
| ---------- | ----------------------------------- | ------------------------------------------------------------- |
| \_rawInput | struct IETS.TaggingRecordRawInput[] | Raw client input data formed as TaggingRecordRawInput struct. |

### removeTags

```solidity
function removeTags(struct IETS.TaggingRecordRawInput[] _rawInput) external payable
```

Remove one or more tags from a tagging record using raw data for record lookup.

| Name       | Type                                | Description                                                   |
| ---------- | ----------------------------------- | ------------------------------------------------------------- |
| \_rawInput | struct IETS.TaggingRecordRawInput[] | Raw client input data formed as TaggingRecordRawInput struct. |

### getOrCreateTagIds

```solidity
function getOrCreateTagIds(string[] _tags) external payable returns (uint256[] _tagIds)
```

Get or create CTAG tokens from tag strings.

Combo function that accepts a tag strings and returns corresponding CTAG token Id if it exists,
or if it doesn't exist, creates a new CTAG and then returns corresponding Id.

Only ETS Relayer contracts may call this function.

| Name   | Type     | Description           |
| ------ | -------- | --------------------- |
| \_tags | string[] | Array of tag strings. |

| Name     | Type      | Description              |
| -------- | --------- | ------------------------ |
| \_tagIds | uint256[] | Array of Id of CTAG Ids. |

### computeTaggingFee

```solidity
function computeTaggingFee(struct IETS.TaggingRecordRawInput _rawInput, enum IETS.TaggingAction _action) external view returns (uint256 fee, uint256 tagCount)
```

Compute tagging fee for raw input and desired action.

| Name       | Type                              | Description                                                                  |
| ---------- | --------------------------------- | ---------------------------------------------------------------------------- |
| \_rawInput | struct IETS.TaggingRecordRawInput | Raw client input data formed as TaggingRecordRawInput struct.                |
| \_action   | enum IETS.TaggingAction           | Integer representing action to be performed according to enum TaggingAction. |

| Name     | Type    | Description                                       |
| -------- | ------- | ------------------------------------------------- |
| fee      | uint256 | Calculated tagging fee in ETH/Matic               |
| tagCount | uint256 | Number of new tags being added to tagging record. |
