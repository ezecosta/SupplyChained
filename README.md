# SupplyChain
Smart contract representing a supply chain with multiple steps for tracking product progress.

## License
This code is licensed under the GPL-3.0 license.

## Overview
This contract allows the registration and tracking of products through various steps in a supply chain. Each product can have multiple steps, and each step is associated with a status, metadata, price, and author.

## Structs
### Step
```solidity
struct Step {
    Status status;
    string metadata;
    uint256 price;
    address author;
}
```
- Represents a step in the supply chain.
- Contains the following fields:
-- status: The current status of the step.
-- metadata: Additional information or metadata related to the step.
-- price: The price associated with the step.
-- author: The address of the author who registered the step.

## Enum
### Status
```solidity
enum Status {
    CREATED,
    READY_FOR_PICK_UP,
    PICKED_UP,
    READY_FOR_DELIVERY,
    DELIVERED
}
```
- Represents the status of a step in the supply chain.
- Possible values are:
  - CREATED: The step is created.
  - READY_FOR_PICK_UP: The product is ready for pick-up.
  - PICKED_UP: The product has been picked up.
  - READY_FOR_DELIVERY: The product is ready for delivery.
  - DELIVERED: The product has been delivered.

## Events
### RegisteredStep
```solidity
event RegisteredStep(
    uint256 productId,
    Status status,
    string metadata,
    address author,
    uint256 price
);
```
- Emitted when a step is registered for a product.
- Provides information about the product ID, status, metadata, author, and price of the step.

## Mapping
### products
```solidity
mapping(uint256 => Step[]) public products;
```
- Maps a product ID to an array of steps.
- Each product can have multiple steps associated with it.

## Functions
### registerProduct
```solidity
function registerProduct(uint256 productId) public returns (bool success)
```
- Registers a new product in the supply chain.
- Requires that the product with the given ID does not already exist.
- Creates the initial step for the product with the status set to CREATED.
- Returns a boolean indicating the success of the operation.

### registerStep
```solidity
function registerStep(uint256 productId, string calldata metadata, uint256 price) public payable returns (bool success)
```
- Registers a new step for a product in the supply chain.
- Requires that the product with the given ID exists.
- Determines the current status based on the previous step's status.
- Checks if the current status allows for a new step.
- Performs validation and payment handling for specific statuses (PICKED_UP and DELIVERED).
- Creates a new step with the provided metadata, price, and sender address.
- Emits the RegisteredStep event with the details of the new step.
- Returns a boolean indicating the success of the operation.

Note: The registerStep function is payable and requires payment for certain statuses (PICKED_UP and DELIVERED).

_This is a simplified explanation of the code. For more details, refer to the code comments._
