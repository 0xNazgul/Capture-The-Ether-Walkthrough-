# Account Takeover

**HINT:** Look up ```0x6B477781b0e68031109f21887e6B5afEAaEB002b``` on [ropsten.etherscan](https://ropsten.etherscan.io/) and look through the transactions. Along with researching a bit about [ECDSA.](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm)
<details>
<summary>Answer</summary>
<p>
After looking through the accounts transactions notice that there are two transactions using the same r value in their signature or k value in ECDSA.

Whats important is that the k value is supposed to be random and must never be reused again. By using the same k more then once for signing different transactions allows for anyone to recompute the private key they used. This happened to Sony in 2010 which you can read up on if your interested.

Once you know this, you can then recompute the private key for ```0x6B477781b0e68031109f21887e6B5afEAaEB002b``` and takeover the account. From there you just import the private key to your metamask and call the ```authenticate()``` function.

* There are a plenty amount of ways to do this and can be found with a simple search.

</p>
</details>