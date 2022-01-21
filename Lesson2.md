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


### What if everyone starts creating zombies(or say any character for a game) infinitely. This will be non sense. So why not to put restriction on making one character/zombie once.

**How can we make it so this function can only be called once per player?**

For that we use **require**. require makes it so that the function will throw an error and stop executing if some condition is not true:

***NOTE - Side note: Solidity doesn't have native string comparison, so we compare their keccak256 hashes to see if the strings are equal) ***


```
function sayHiToVitalik(string memory _name) public returns (string memory) {

  // Compares if _name equals "Vitalik". Throws an error and exits if not true.
  // (Side note: Solidity doesn't have native string comparison, so we
  // compare their keccak256 hashes to see if the strings are equal)
  
  require(keccak256(abi.encodePacked(_name)) == keccak256(abi.encodePacked("Vitalik")));   //dont forget to put semicolon here
  
  // If it's true, proceed with the function:
  //if the zombie we are looking for is "Vitalik", say Hii, if it is vitalik, then hash or passed name and Vitalik must be same
  
  return "Hi!";
}
```
#### Thus require is quite useful for verifying certain conditions that must be true before running a function.

## Chapter 5: Inheritance
As we have read in OOPS principles, we can inherit or reuse our code. It saves us from writing same code again and code becomes more manageable.
Also we can inherit all that which is useful to us.

```
contract Doge {
  function catchphrase() public returns (string memory) {
    return "So Wow CryptoDoge";
  }
}
//contract BabyDoge is ineriting Doge
contract BabyDoge is Doge {
  function anotherCatchphrase() public returns (string memory) {
    return "Such Moon BabyDoge";
  }
}
```

In solidity we use "is" keyword to inherit a contract. In cpp we used semicolons, in java we use extends.

## Chapter 6: Import
We have seen how import works in java, similar to that, we will use it in solidity. When we want to import something ffrom other files, we can use it. 

When you have multiple files and you want to import one file into another, Solidity uses the import keyword:
```
import "./someothercontract.sol";
// we are not specifying the entire path, because the file is in same directory as the one we are working in

contract newContract is SomeOtherContract {

}
```

**So if we had a file named someothercontract.sol in the same directory as this contract (that's what the ./ means), it would get imported by the compiler.**

```
pragma solidity >=0.5.0 <0.6.0;

// we are writing this statement after solidity version and not above that
import "./zombiefactory.sol";

contract ZombieFeeding is ZombieFactory {

}

```

## Chapter 7: Storage vs Memory (Data location)

Storage refers to variables stored permanently on the blockchain. 

Memory variables are temporary, and are erased between external function calls to your contract.

Solidity handles them by default. State variables (variables declared outside of functions) are by default storage and written permanently to the blockchain, while variables declared inside functions are memory and will disappear when the function call ends.

When dealing with structs and arrays within functions, we need to use these words:

## Chapter 8  Internal and External

In addition to public and private, Solidity has two more types of visibility for functions: internal and external.

**internal is the same as private, except that it's also accessible to contracts that inherit from this contract.**

**external is similar to public, except that these functions can ONLY be called outside the contract — they can't be called by other functions inside that contract.**


