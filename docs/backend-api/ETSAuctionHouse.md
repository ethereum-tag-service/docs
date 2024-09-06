# ETSAuctionHouse

ETSAuctionHouse contract governs the sale of Ethereum Tag Service composable tags (CTAGs).

## Functions

### constructor

```solidity
constructor() public
```

### initialize

```solidity
function initialize(contract IETSToken _etsToken, contract IETSAccessControls _etsAccessControls, address _wmatic, uint256 _timeBuffer, uint256 _reservePrice, uint8 _minBidIncrementPercentage, uint256 _duration, uint256 _relayerPercentage, uint256 _platformPercentage) external
```

### \_authorizeUpgrade

```solidity
function _authorizeUpgrade(address) internal
```

### pause

```solidity
function pause() public
```

### unpause

```solidity
function unpause() public
```

### setDuration

```solidity
function setDuration(uint256 _duration) public
```

### setMinBidIncrementPercentage

```solidity
function setMinBidIncrementPercentage(uint8 _minBidIncrementPercentage) public
```

### setReservePrice

```solidity
function setReservePrice(uint256 _reservePrice) public
```

### setTimeBuffer

```solidity
function setTimeBuffer(uint256 _timeBuffer) public
```

### setProceedPercentages

```solidity
function setProceedPercentages(uint256 _platformPercentage, uint256 _relayerPercentage) public
```

### createBid

```solidity
function createBid(uint256 _tokenId) public payable
```

### settleAuction

```solidity
function settleAuction(uint256 _tokenId) public
```

### \_safeTransferETHWithFallback

```solidity
function _safeTransferETHWithFallback(address to, uint256 amount) internal
```

### \_safeTransferETH

```solidity
function _safeTransferETH(address to, uint256 value) internal returns (bool)
```

### \_exists

```solidity
function _exists(uint256 _tokenId) internal view returns (bool)
```

### auctionActive

```solidity
function auctionActive(uint256 _tokenId) public view returns (bool)
```

### getAuction

```solidity
function getAuction(uint256 _tokenId) public view returns (struct IETSAuctionHouse.Auction)
```

### receive

```solidity
receive() external payable
```

### fallback

```solidity
fallback() external payable
```
