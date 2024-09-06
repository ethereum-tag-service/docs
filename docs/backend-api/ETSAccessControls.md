# ETSAccessControls

This is the interface for the ETSAccessControls contract which allows ETS Core Dev
Team to administer roles and control access to various parts of the ETS Platform.
ETSAccessControls contract contains a mix of public and administrator only functions.

## Functions

### constructor

```solidity
constructor() public
```

### initialize

```solidity
function initialize(address _platformAddress) public
```

### \_authorizeUpgrade

```solidity
function _authorizeUpgrade(address) internal
```

### setPlatform

```solidity
function setPlatform(address payable _platform) public
```

Sets the Platform wallet address. Can only be called by address with DEFAULT_ADMIN_ROLE.

| Name       | Type            | Description                      |
| ---------- | --------------- | -------------------------------- |
| \_platform | address payable | The new Platform address to set. |

### setRoleAdmin

```solidity
function setRoleAdmin(bytes32 _role, bytes32 _adminRole) public
```

Sets the role admin for a given role. An address with role admin can grant or
revoke that role for other addresses. Can only be called by address with DEFAULT_ADMIN_ROLE.

| Name        | Type    | Description                                        |
| ----------- | ------- | -------------------------------------------------- |
| \_role      | bytes32 | bytes32 representation of role being administered. |
| \_adminRole | bytes32 | bytes32 representation of administering role.      |

### addRelayer

```solidity
function addRelayer(address _relayer, string _name) public
```

Adds a Relayer contract to ETS. Can only be called by address
with DEFAULT_ADMIN_ROLE.

| Name      | Type    | Description                                                   |
| --------- | ------- | ------------------------------------------------------------- |
| \_relayer | address | Address of the Relayer contract. Must conform to IETSRelayer. |
| \_name    | string  | Human readable name of the Relayer.                           |

### toggleIsRelayerPaused

```solidity
function toggleIsRelayerPaused(address _relayer) public
```

Pauses/Unpauses a Relayer contract. Can only be called by address
with DEFAULT_ADMIN_ROLE.

| Name      | Type    | Description                      |
| --------- | ------- | -------------------------------- |
| \_relayer | address | Address of the Relayer contract. |

### isSmartContract

```solidity
function isSmartContract(address _addr) public view returns (bool)
```

Checks whether given address has SMART_CONTRACT role.

| Name   | Type    | Description            |
| ------ | ------- | ---------------------- |
| \_addr | address | Address being checked. |

| Name | Type | Description                                      |
| ---- | ---- | ------------------------------------------------ |
| [0]  | bool | boolean True if address has SMART_CONTRACT role. |

### isAdmin

```solidity
function isAdmin(address _addr) public view returns (bool)
```

Checks whether given address has DEFAULT_ADMIN_ROLE role.

| Name   | Type    | Description            |
| ------ | ------- | ---------------------- |
| \_addr | address | Address being checked. |

| Name | Type | Description                                          |
| ---- | ---- | ---------------------------------------------------- |
| [0]  | bool | boolean True if address has DEFAULT_ADMIN_ROLE role. |

### isRelayer

```solidity
function isRelayer(address _addr) public view returns (bool)
```

Checks whether given address has PUBLISHER role.

| Name   | Type    | Description            |
| ------ | ------- | ---------------------- |
| \_addr | address | Address being checked. |

| Name | Type | Description                                 |
| ---- | ---- | ------------------------------------------- |
| [0]  | bool | boolean True if address has PUBLISHER role. |

### isRelayerAdmin

```solidity
function isRelayerAdmin(address _addr) public view returns (bool)
```

Checks whether given address has PUBLISHER_ADMIN role.

| Name   | Type    | Description            |
| ------ | ------- | ---------------------- |
| \_addr | address | Address being checked. |

| Name | Type | Description                                       |
| ---- | ---- | ------------------------------------------------- |
| [0]  | bool | boolean True if address has PUBLISHER_ADMIN role. |

### isRelayerByName

```solidity
function isRelayerByName(string _name) public view returns (bool)
```

Checks whether given Relayer Name is a registered Relayer.

| Name   | Type   | Description         |
| ------ | ------ | ------------------- |
| \_name | string | Name being checked. |

| Name | Type | Description                          |
| ---- | ---- | ------------------------------------ |
| [0]  | bool | boolean True if \_name is a Relayer. |

### isRelayerByAddress

```solidity
function isRelayerByAddress(address _addr) public view returns (bool)
```

Checks whether given address is a registered Relayer.

| Name   | Type    | Description            |
| ------ | ------- | ---------------------- |
| \_addr | address | Address being checked. |

| Name | Type | Description                                      |
| ---- | ---- | ------------------------------------------------ |
| [0]  | bool | boolean True if address is a registered Relayer. |

### isRelayerAndNotPaused

```solidity
function isRelayerAndNotPaused(address _addr) public view returns (bool)
```

Checks whether given address is a registered Relayer and not paused.

| Name   | Type    | Description            |
| ------ | ------- | ---------------------- |
| \_addr | address | Address being checked. |

| Name | Type | Description                                          |
| ---- | ---- | ---------------------------------------------------- |
| [0]  | bool | boolean True if address is a Relayer and not paused. |

### getRelayerAddressFromName

```solidity
function getRelayerAddressFromName(string _name) public view returns (address)
```

Get relayer address from it's name.

| Name   | Type   | Description      |
| ------ | ------ | ---------------- |
| \_name | string | Name of relayer. |

| Name | Type    | Description         |
| ---- | ------- | ------------------- |
| [0]  | address | Address of relayer. |

### getRelayerNameFromAddress

```solidity
function getRelayerNameFromAddress(address _address) public view returns (string)
```

Get relayer name from it's address.

| Name      | Type    | Description          |
| --------- | ------- | -------------------- |
| \_address | address | Adsdress of relayer. |

| Name | Type   | Description      |
| ---- | ------ | ---------------- |
| [0]  | string | Name of relayer. |

### getPlatformAddress

```solidity
function getPlatformAddress() public view returns (address payable)
```

Returns wallet address for ETS Platform.

| Name | Type            | Description           |
| ---- | --------------- | --------------------- |
| [0]  | address payable | ETS Platform address. |
