# Mapping

**HINT:** Look at how the mapping works in the ```set()``` function.
<details>
<summary>Answer</summary>
<p>

* Use the ```set()``` function to set a random value at a key of 2**256-2
    * ```0x0000000000000000000000000000000000000000000000000000000000000001```
* Go to your contract on [ropsten.etherscan](https://ropsten.etherscan.io/)
    * Click on your Tx and look at the storage address of your tx
    * Mine was: ```0xb10e2d527612073b26eecdfd717e6a320cf44b4afac2b0732d9fcbe2b7fa0cf6```
* Calculate the key anyway you choose (I did it in Python).
    * Yours will be different
```py
print('0x{0:02x}'.format(2**256 - Storage_Address))
"0x4ef1d2ad89edf8c4d91132028e8195cdf30bb4b5053d4f8cd260341d4805f30a"
```
* Use the ```set()``` function again with you calculated key and ```0x0000000000000000000000000000000000000000000000000000000000000001``` as the value
</p>
</details>