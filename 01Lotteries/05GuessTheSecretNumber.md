# Guess The Secret Number

**HINT:** Create a contract that calculates the bytes32 hash as a number
<details>
<summary>Part 1</summary>
<p>
First we need to find the correct answer 

```
pragma solidity ^0.4.21;

contract NumSolution {
    bytes32 secret = 0xdb81b4d58595fbbbb592d3661a34cdca14d7ab379441400cbfa1b78bc447c365;
        
        function check() public view returns (uint8) {
            for(uint8 i; i<256; i++) {
                if(keccak256(i) == secret) {
                    return i;
                }
            }
        }
}
```

</p>
</details>

<details>
<summary>Part 2</summary>
<p>

* Copy the contract and paste it into Remix IDE 
* Click on ```deploy at``` with your contract instance address 
* Input the answer you found with your other smart contract (170)

</p>
</details>
