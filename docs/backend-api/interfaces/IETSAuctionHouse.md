# IETSAuctionHouse

This is the standard interface for the ETSAuctionHouse.sol contract. It includes both public
and administration functions.

## Functions

### pause

```solidity
function pause() external
```

### unpause

```solidity
function unpause() external
```

### setReservePrice

```solidity
function setReservePrice(uint256 _reservePrice) external
```

### setTimeBuffer

```solidity
function setTimeBuffer(uint256 timeBuffer) external
```

### setProceedPercentages

```solidity
function setProceedPercentages(uint256 _platformPercentage, uint256 _relayerPercentage) external
```

### createBid

```solidity
function createBid(uint256 auctionId) external payable
```

### getAuction

```solidity
function getAuction(uint256 _tokenId) external returns (struct IETSAuctionHouse.Auction auction)
```

### settleAuction

```solidity
function settleAuction(uint256 _tokenId) external
```

## Events

### AuctionBid

```solidity
event AuctionBid(uint256 tokenId, address sender, uint256 value, bool extended)
```

### AuctionCreated

```solidity
event AuctionCreated(uint256 tokenId)
```

### AuctionExtended

```solidity
event AuctionExtended(uint256 tokenId, uint256 endTime)
```

### AuctionSettled

```solidity
event AuctionSettled(uint256 tokenId, address winner, uint256 totalProceeds, uint256 relayerProceeds, uint256 creatorProceeds)
```

### AuctionDurationSet

```solidity
event AuctionDurationSet(uint256 duration)
```

### AuctionMinBidIncrementPercentageSet

```solidity
event AuctionMinBidIncrementPercentageSet(uint8 minBidIncrementPercentagePrice)
```

### AuctionReservePriceSet

```solidity
event AuctionReservePriceSet(uint256 reservePrice)
```

### AuctionTimeBufferSet

```solidity
event AuctionTimeBufferSet(uint256 timeBuffer)
```

### AuctionProceedPercentagesSet

```solidity
event AuctionProceedPercentagesSet(uint256 platformPercentage, uint256 relayerPercentage, uint256 creatorPercentage)
```
