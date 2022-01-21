## Chapter 2: Mappings and Addresses

We'll work with 2 new data types: **mapping and address.**

### Addresses

The Ethereum blockchain is made up of accounts, which you can think of like bank accounts. 

An account has a balance of Ether (the currency used on the Ethereum blockchain), and you can send and receive Ether payments to other accounts, just like your bank account can wire transfer money to other bank accounts.

Each account has an address, which you can think of like a bank account number. It's a unique identifier that points to that account, and it looks like this:

0x0cE446255506E92DF41614C46F1d6df9Cc969183

### Mappings 
Mappings are another way of storing organized data in Solidity, like structs and arrays.
Its like a map we see in C++ STL. There is a key value pair.

Defining a mapping looks like this:

```
// For a financial app, storing a uint that holds the user's account balance:
mapping (address => uint) public accountBalance;
//(SPACE MATTERS A LOT IN mapping and (Address---)
// Or could be used to store / lookup usernames based on userId
mapping (uint => string) userIdToName;
```

A mapping is essentially a key-value store for storing and looking up data. In the first example, the key is an address and the value is a uint, and in the second example the key is a uint and the value a string.


### Chapter 3: Msg.sender

msg.sender
In Solidity, there are certain global variables that are available to all functions. One of these is msg.sender, which refers to the address of the person (or smart contract) who called the current function. 
(As we have read in java, the object class and its member are accessible to all the class, here also, there are some global variable available for all the functions to use).

Note: In Solidity, function execution always needs to start with an external caller. A contract will just sit on the blockchain doing nothing until someone calls one of its functions. So there will always be a msg.sender. In other languages also, function needs to be called for executing it. Lets keep the recursion aside for some time, surely there will be something like recursion in solidity, me may get to see it in upcoming lessons. Even in recursion also, function needs to be called...

```
mapping (address => uint) favoriteNumber;

function setMyNumber(uint _myNumber) public {
  // Update our `favoriteNumber` mapping to store `_myNumber` under `msg.sender`
  favoriteNumber[msg.sender] = _myNumber;
  // ^ The syntax for storing data in a mapping is just like with arrays
}

function whatIsMyNumber() public view returns (uint) {
  // Retrieve the value stored in the sender's address
  // Will be `0` if the sender hasn't called `setMyNumber` yet
  return favoriteNumber[msg.sender];
}
```
Using msg.sender gives you the security of the Ethereum blockchain — the only way someone can modify someone else's data would be to steal the private key associated with their Ethereum address.

**msg.sender contains the address that has originated the call while tx.origin contains the originator of the transaction.**

According to an answer on stackoverflow,
msg.sender will be the person who's currently connecting with the contract.
Later on, you'll probably deal with contracts connecting with contracts. In that case, the contract that is creating the call would be the msg.sender.



