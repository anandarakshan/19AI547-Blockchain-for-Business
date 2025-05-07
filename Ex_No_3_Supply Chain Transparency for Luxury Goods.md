# Aim:
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
# Algorithm:
Step 1:
Manufacturer inputs productId and name, and registers the product if it's not already registered.

Step 2:
Contract stores the product with name, msg.sender as currentOwner, and sets verified = true.

Step 3:
For ownership transfer, contract checks if msg.sender is the current owner of the product.

Step 4:
If valid, contract updates currentOwner to the new owner's address and emits an event.

Step 5:
Repeat the ownership transfer at each supply chain checkpoint by authorized parties.

Step 6:
Buyer or verifier inputs productId to retrieve product details from the smart contract.

Step 7:
Contract returns the product’s name, currentOwner, and verified status for authenticity check.

Step 8:
All actions (registration and transfers) are permanently recorded on-chain for transparency and trust.

# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LuxurySupplyChain {
    struct Product {
        string name;
        address currentOwner;
        bool verified;
    }

    mapping(uint256 => Product) public products;

    event ProductRegistered(uint256 productId, string name);
    event OwnershipTransferred(uint256 productId, address newOwner);

    function registerProduct(uint256 productId, string memory name) public {
        require(products[productId].currentOwner == address(0), "Product already registered");
        products[productId] = Product(name, msg.sender, true);
        emit ProductRegistered(productId, name);
    }

    function transferOwnership(uint256 productId, address newOwner) public {
        require(products[productId].currentOwner == msg.sender, "Not the owner");
        products[productId].currentOwner = newOwner;
        emit OwnershipTransferred(productId, newOwner);
    }

    function verifyProduct(uint256 productId) public view returns (string memory, address, bool) {
        Product memory p = products[productId];
        return (p.name, p.currentOwner, p.verified);
    }
}
```
# Expected Output:
1.A luxury good (e.g., a Rolex watch) is registered on-chain.


2.Ownership is transferred at every checkpoint.


3.Buyers can check the authenticity before purchasing.


# High-Level Overview:
1.Helps prevent counterfeit luxury goods.


2.Teaches real-world supply chain use cases.

# OUTPUT:
![alt text](<Screenshot 2025-04-24 114106.png>)
### For Register:
![alt text](<Screenshot 2025-04-24 122816.png>)
### For Transfer Ownership:
![alt text](<Screenshot 2025-04-24 122857.png>)
### For Verification:
![alt text](<Screenshot 2025-04-24 122919.png>)
# RESULT : 
Thus, a smart contract that tracks the supply chain of luxury goods and ensuring authenticity is successfully executed.
