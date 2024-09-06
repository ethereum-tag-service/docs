# UintArrayUtils

## Functions

### indexOf

```solidity
function indexOf(uint256[] A, uint256 a) internal pure returns (uint256, bool)
```

Finds the index of the first occurrence of the given element.

| Name | Type | Description |
| ---- | ---- | ----------- |
| A | uint256[] | The input array to search |
| a | uint256 | The value to find |

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256 | Returns (index and isIn) for the first occurrence starting from index 0 |
| [1] | bool |  |

### contains

```solidity
function contains(uint256[] A, uint256 a) internal pure returns (bool)
```

Returns true if the value is present in the list. Uses indexOf internally.

| Name | Type | Description |
| ---- | ---- | ----------- |
| A | uint256[] | The input array to search |
| a | uint256 | The value to find |

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | bool | Returns isIn for the first occurrence starting from index 0 |

### difference

```solidity
function difference(uint256[] A, uint256[] B) internal pure returns (uint256[])
```

Computes the difference of two arrays. Assumes there are no duplicates.

| Name | Type | Description |
| ---- | ---- | ----------- |
| A | uint256[] | The first array |
| B | uint256[] | The second array |

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256[] | A - B; an array of values in A not found in B. |

### intersect

```solidity
function intersect(uint256[] A, uint256[] B) internal pure returns (uint256[])
```

Returns the intersection of two arrays. Arrays are treated as collections, so duplicates are kept.

| Name | Type | Description |
| ---- | ---- | ----------- |
| A | uint256[] | The first array |
| B | uint256[] | The second array |

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256[] | The intersection of the two arrays |

### extend

```solidity
function extend(uint256[] A, uint256[] B) internal pure returns (uint256[])
```

Returns the combination of two arrays

| Name | Type | Description |
| ---- | ---- | ----------- |
| A | uint256[] | The first array |
| B | uint256[] | The second array |

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | uint256[] | Returns A extended by B |

