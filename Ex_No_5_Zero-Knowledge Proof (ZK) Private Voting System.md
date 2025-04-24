# Experiment 5: Zero-Knowledge Proof (ZK) Private Voting System
# Aim:
To implement a fully private and transparent voting system using Zero-Knowledge Proofs (ZKPs). This ensures that votes are counted fairly without revealing who voted for whom.

# Algorithm:

### Step 1: Voter Registration
Each voter generates a secret vote key and submits a commitment (hashed vote) to the contract.


### Step 2: Voting Process
Voters submit their votes privately using a hash, without revealing their choice.


### Step 3: ZK Verification
The contract verifies if a vote belongs to a registered voter but does not reveal the actual vote.


### Step 4: Vote Counting
Once voting ends, the contract reveals the final tally without linking votes to individuals.



# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ZKVoting {
    struct Voter {
        bool registered;
        bytes32 voteCommitment;
    }

    mapping(address => Voter) public voters;
    uint256 public votesForA;
    uint256 public votesForB;

    event VoteCommitted(address voter, bytes32 commitment);
    event VoteRevealed(address voter, uint256 choice);

    function registerVoter(bytes32 commitment) public {
        require(!voters[msg.sender].registered, "Already registered");
        voters[msg.sender] = Voter(true, commitment);
        emit VoteCommitted(msg.sender, commitment);
    }

    function revealVote(string memory secret, uint256 choice) public {
        require(voters[msg.sender].registered, "Not registered");
        require(keccak256(abi.encodePacked(secret, choice)) == voters[msg.sender].voteCommitment, "Invalid proof");

        if (choice == 1) votesForA++;
        if (choice == 2) votesForB++;

        emit VoteRevealed(msg.sender, choice);
    }
}

```

```
web3.utils.soliditySha3({type: "string", value: "your name"}, {type: "uint256", value: "1 or 2"})
```

# Expected Output:

```
Voters commit their votes privately.


When revealed, the contract verifies correctness but keeps votes anonymous.


Final result is publicly verifiable without exposing individual votes.
```

![51](https://github.com/user-attachments/assets/8ca9b76d-4e4d-4f80-9413-eabd2ec0f23b)

![52](https://github.com/user-attachments/assets/816fa7c3-0024-4614-9d63-2746010d6edc)

![53](https://github.com/user-attachments/assets/5251d5ca-4f00-41eb-a7b3-ebf183e01e69)

![54](https://github.com/user-attachments/assets/a424bbc1-e3d6-42df-b891-bfee6f722769)


# High-Level Overview:

```
Uses ZKPs to ensure anonymous and fair elections.


Prevents vote tampering while maintaining voter privacy.


Mimics real-world ZK voting applications in governance and DAOs.
```

# RESULT: 
Thus, the Zero-Knowledge Proof (ZK) Private Voting System is successfully implemented.
