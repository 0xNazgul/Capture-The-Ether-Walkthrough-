# Token Sale

**HINT:** Look at how the contract sets the ```PRICE_PER-TOKEN``` and how it can be manipulated in the ```buy()``` function.
<details>
<summary>Answer</summary>
<p>

Your going to want to overflow the uint256 value of ```PRICE_PER-TOKEN.``` To do so you must calulate the amount of tokens to buy and how much wei to send with it.
* Max value of uint256 if 2**256-1
* 1 ether to wei is 10**18
* To find the numTokens to buy we:
    * ```((2**256)-1) / (10**18)```
    * ```115792089237316195423570985008687907853269984665640564039458```
* To find the amount of wei to send with it we:
    * ```(((2**256)-1) / (10**18)) - ((2*256)-1))```
    * ```415992086870360064``` wei
* Now just buy ```115792089237316195423570985008687907853269984665640564039458``` Tokens, with ```415992086870360064``` wei
* Then sell 1 token and you get 1 ether



</p>
</details>