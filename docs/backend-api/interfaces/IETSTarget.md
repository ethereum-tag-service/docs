# IETSTarget

This is the standard interface for the core ETSTarget.sol contract. It includes both public
and administration functions.

In ETS, a "Target" is our data structure, stored onchain, that references/points to a URI. Target records
are identified in ETS by their Id (targetId) which is a unsigned integer computed from the URI string.
Target Ids are combined with CTAG Ids by ETS core (ETS.sol) to form "Tagging Records".

For context, from Wikipedia, URI is short for Uniform Resource Identifier and is a unique sequence of
characters that identifies a logical or physical resource used by web technologies. URIs may be used to
identify anything, including real-world objects, such as people and places, concepts, or information
resources such as web pages and books.

For our purposes, as much as possible, we are restricting our interpretation of URIs to the more technical
parameters defined by the IETF in [RFC3986](https://www.rfc-editor.org/rfc/rfc3986). For newer protocols, such
as blockchains, For newer protocols, such as blockchains we will lean on newer emerging URI standards such
as the [Blink](https://w3c-ccg.github.io/blockchain-links) and [BIP-122](https://github.com/bitcoin/bips/blob/master/bip-0122.mediawiki)

One the thing to keep in mind with URIs & ETS Targets is that differently shaped URIs can sometimes point to the same
resource. The effect of that is that different Target IDs in ETS can similarly point to the same resource.

## Functions

### setEnrichTarget

```solidity
function setEnrichTarget(address _etsEnrichTarget) external
```

Sets ETSEnrichTarget contract address so that Target metadata enrichment
functions can be called from ETSTarget.

| Name | Type | Description |
| ---- | ---- | ----------- |
| _etsEnrichTarget | address | Address of ETSEnrichTarget contract. |

### getOrCreateTargetId

```solidity
function getOrCreateTargetId(string _targetURI) external returns (uint256)
```

Get ETS targetId from URI.

Combo function that given a URI string will return it's ETS targetId if it exists,
or create a new Target record and return corresponding targetId.

| Name | Type | Description |
| ---- | ---- | ----------- |
| _targetURI | string | URI passed in as string |

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | Id of ETS Target record |

### createTarget

```solidity
function createTarget(string _targetURI) external returns (uint256 targetId)
```

Create a Target record and return it's targetId.

| Name | Type | Description |
| ---- | ---- | ----------- |
| _targetURI | string | URI passed in as string |

| Name | Type | Description |
| ---- | ---- | ----------- |
| targetId | uint256 | Id of ETS Target record |

### updateTarget

```solidity
function updateTarget(uint256 _targetId, string _targetURI, uint256 _enriched, uint256 _httpStatus, string _ipfsHash) external returns (bool success)
```

Update a Target record.

| Name | Type | Description |
| ---- | ---- | ----------- |
| _targetId | uint256 | Id of Target being updated. |
| _targetURI | string | Unique resource identifier Target points to. |
| _enriched | uint256 | block timestamp when Target was last enriched |
| _httpStatus | uint256 | https status of last response from ETSEnrichTarget API eg. "404", "200". defaults to 0 |
| _ipfsHash | string | ipfsHash of additional metadata for Target collected by ETSEnrichTarget API |

| Name | Type | Description |
| ---- | ---- | ----------- |
| success | bool | true when Target is successfully updated. |

### computeTargetId

```solidity
function computeTargetId(string _targetURI) external view returns (uint256 targetId)
```

Function to deterministically compute & return a targetId.

Every Target in ETS is mapped to by it's targetId. This Id is computed from
the target URI sting hashed and cast as a uint256.

Note: Function does not verify if Target record exists.

| Name | Type | Description |
| ---- | ---- | ----------- |
| _targetURI | string | Unique resource identifier Target record points to. |

| Name | Type | Description |
| ---- | ---- | ----------- |
| targetId | uint256 | Id of the potential Target record. |

### targetExistsByURI

```solidity
function targetExistsByURI(string _targetURI) external view returns (bool)
```

Check that a Target record exists for a given URI string.

| Name | Type | Description |
| ---- | ---- | ----------- |
| _targetURI | string | Unique resource identifier Target record points to. |

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | bool | true if Target record exists; false if not. |

### targetExistsById

```solidity
function targetExistsById(uint256 _targetId) external view returns (bool)
```

Check that a Target record exists for a given computed targetId.

| Name | Type | Description |
| ---- | ---- | ----------- |
| _targetId | uint256 | targetId uint computed from URI via computeTargetId(). |

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | bool | true if Target record exists; false if not. |

### getTargetByURI

```solidity
function getTargetByURI(string _targetURI) external view returns (struct IETSTarget.Target)
```

Retrieve a Target record for a given URI string.

Note: returns a struct with empty members when no Target exists.

| Name | Type | Description |
| ---- | ---- | ----------- |
| _targetURI | string | Unique resource identifier Target record points to. |

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | struct IETSTarget.Target | Target record. |

### getTargetById

```solidity
function getTargetById(uint256 _targetId) external view returns (struct IETSTarget.Target)
```

Retrieve a Target record for a computed targetId.

Note: returns a struct with empty members when no Target exists.

| Name | Type | Description |
| ---- | ---- | ----------- |
| _targetId | uint256 | targetId uint computed from URI via computeTargetId(). |

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | struct IETSTarget.Target | Target record. |

## Events

### AccessControlsSet

```solidity
event AccessControlsSet(address etsAccessControls)
```

_emitted when the ETSAccessControls is set._

| Name | Type | Description |
| ---- | ---- | ----------- |
| etsAccessControls | address | contract address ETSAccessControls is set to. |

### EnrichTargetSet

```solidity
event EnrichTargetSet(address etsEnrichTarget)
```

_emitted when the ETSEnrichTarget API address is set._

| Name | Type | Description |
| ---- | ---- | ----------- |
| etsEnrichTarget | address | contract address ETSEnrichTarget is set to. |

### TargetCreated

```solidity
event TargetCreated(uint256 targetId)
```

_emitted when a new Target is created._

| Name | Type | Description |
| ---- | ---- | ----------- |
| targetId | uint256 | Unique Id of new Target. |

### TargetUpdated

```solidity
event TargetUpdated(uint256 targetId)
```

_emitted when an existing Target is updated._

| Name | Type | Description |
| ---- | ---- | ----------- |
| targetId | uint256 | Id of Target being updated. |

