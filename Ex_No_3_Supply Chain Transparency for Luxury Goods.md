# Aim:
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
# Algorithm:
The manufacturer records product creation details on-chain.


The product moves through different supply chain checkpoints.


The ownership of the product can be transferred securely.


Buyers can verify the product’s authenticity.


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

```
A luxury good (e.g., a Rolex watch) is registered on-chain.

Ownership is transferred at every checkpoint.

Buyers can check the authenticity before purchasing.
```

![3aaa](https://github.com/user-attachments/assets/f352711a-de77-492c-86b3-e2a557ee5e94)

![3bbb](https://github.com/user-attachments/assets/53a10fa3-c91e-411a-b103-cf04dee2ad54)

![3ccc](https://github.com/user-attachments/assets/eb6ceef2-82e7-47ed-9185-b70f4a5bc598)


# High-Level Overview:

```
Helps prevent counterfeit luxury goods.

Teaches real-world supply chain use cases.
```

# RESULT : 

Thus, the Supply Chain Transparency for Luxury Goods has been implemented successfully.
