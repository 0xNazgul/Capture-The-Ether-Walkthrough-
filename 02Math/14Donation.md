# Donation

**HINT:** Check out how the the ```donate()``` function calculate the ```scale``` variable
<details>
<summary>Answer</summary>
<p>

We can see that ```scale``` is calculated as:
```
10**18 * 1 ether
1 ether is 10**18 wei 
10**18 * 10**18
10**36
```
So all we have to do take over the contract is:
* convert you address from a hex to number
* Divide you address by 10**36 (completely leaving out the decimal numbers)
* Use the ```donate()``` function with the number you calculated for the value in wei and your address for the ```etherAmount```

</p>
</details>
