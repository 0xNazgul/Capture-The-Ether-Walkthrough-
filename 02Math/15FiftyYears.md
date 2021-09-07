# Fifty Years

**HINT:** Figure out how to manipulate ```upsert()``` function and the ```withdraw()``` function
<details>
<summary>Answer</summary>
<p>
We pretty much overflow the unlockTimestamp along with overwriting the length variable in the contracts array. Here is the sequence we need to do:

* Call ```upsert()``` with ```index:1``` ```timestamp:2**256-86400``` and  1 wei
* Call ```upsert()``` with ```index:2``` ```timestamp:0``` and  2 wei
* Call ```upsert()``` with ```index:3``` ```timestamp:86400``` and  3 wei
* Call ```upsert()``` with ```index:4``` ```timestamp:2**256-86400``` and  4 wei
* Call ```upsert()``` with ```index:5``` ```timestamp:0``` and  5 wei
* Call ```withdraw()``` with ```index:3``` NO wei
<br></br>

This leaves us with 6 wei left in the contract. To retrieve that we do this sequence 6 times:
* Call ```upsert()``` with ```index:0```  ```timestamp:2**256-86400```
* Call ```upsert()``` with ```index:1```  ```timestamp:0```
* Call ```withdraw()``` with ```index:0``` 

</p>
</details>
