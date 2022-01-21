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



