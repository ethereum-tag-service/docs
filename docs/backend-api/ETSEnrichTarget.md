# ETSEnrichTarget

Contract that handles the enrichment of Target metadata using off-chain APIs.

In order to keep the on-chain recording of new Target records lightweight and inexpensive,
the createTarget() function (ETSTarget.sol) requires only a URI string (targetURI).

To augment this, we are developing a hybrid onchain/off-chain Enrich Target flow for the purpose of
collecting additional metadata about a Target and saving it back on-chain.

The flow begins with the requestEnrichTarget() function (see below) which takes a targetId as an
argument. If the Target exists, the function emits the targetId via the RequestEnrichTarget event.

An OpenZeppelin Defender Sentinel is listening for this event, and when detected, passes the
targetId to an ETS off-chain service we call the Enrich Target API, which extracts the Target URI,
collects metadata about the URI and saves it in json format to IPFS. The IPFS entpoint is posted
back on-chain via fulfillEnrichTarget() thus updating the Target data struct.

Future implementation should utilize ChainLink in place of OpenZeppelin for better decentralization.

## Functions

### constructor

```solidity
constructor() public
```

### initialize

```solidity
function initialize(contract IETSAccessControls _etsAccessControls, contract IETSTarget _etsTarget) public
```

### _authorizeUpgrade

```solidity
function _authorizeUpgrade(address) internal
```

### requestEnrichTarget

```solidity
function requestEnrichTarget(uint256 _targetId) public
```

Request enrichment for a Target using the hybrid ETS Enrich Target API.

| Name | Type | Description |
| ---- | ---- | ----------- |
| _targetId | uint256 | Id of Target being enriched. |

### fulfillEnrichTarget

```solidity
function fulfillEnrichTarget(uint256 _targetId, string _ipfsHash, uint256 _httpStatus) public
```

Updates Target record with additional metadata stored behind IPFS hash.

| Name | Type | Description |
| ---- | ---- | ----------- |
| _targetId | uint256 | Id of Target being enriched & updated. |
| _ipfsHash | string | IPFS hash with metadata related to the Target. |
| _httpStatus | uint256 | HTTP response code from off-chain ETS Enrich Target API. |

