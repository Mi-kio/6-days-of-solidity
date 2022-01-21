### Chapter 1 -
Overview - Going to build a "Zombie Factory" to build an army of zombies.

### Chapter 2 - 
Solidity code is encapsulated in **contracts**. The word encapsulation means encapsulating/binding something in a single unit, which is also an OOP concept. 
As in OOP we encapsulate code in classes, here we encapsulate it in **contracts**. 

1. What is contract?
 A contract is the fundamental building block of Ethereum applications. (Sounds similar to definition of class in OOPS, where classes are building blocks of OOP)
 All data members and member func are enclosed in a class in OOP and here **all variable and functions are enclosed in a contract.**
 
Declaration of a contract- (Space matters!)
```
contract HelloWorld {

}
```

2. Version Pragma

All solidity source code should start with a "version pragma" — a declaration of the version of the Solidity compiler this code should use. 

This is to prevent issues with future compiler versions potentially introducing changes that would break your code.

As we declare header files in cpp programs, import classes and modules in Java and Python, here we start our code with **Version Pragna**. 

pragma solidity >=0.5.0 <0.6.0; means that we'll be able to compile smart contracts with any compiler version in the range of 0.5.0 (inclusive) to 0.6.0 (exclusive).


```
pragma solidity >=0.5.0 <0.6.0;

contract HelloWorld {

}
```

### Chapter 3 -  State Variables & Integers

State variables are permanently stored in contract storage. This means they're written to the Ethereum blockchain.

 ```
 Example:
contract Example {
  // This will be stored permanently in the blockchain
  uint myUnsignedInteger = 100;
}
 ```
 
 **The uint data type is an unsigned integer, meaning its value must be non-negative. There's also an int data type for signed integers.**
 
 Similar to variable declaration in any other language, here we write **Datatype-Name = Value;**
 
 ### Chapter 4: Math Operations
 
Addition: x + y

Subtraction: x - y

Multiplication: x * y

Division: x / y

Modulus / remainder: x % y 

Exponential Operator: x ** y; // equal to x^y


## Chapter 5: Structs

We have read **structure** in C++, but Solidity also offers structures to us and the purpose is same, to **handle complex data type**. We used structure for making nodes of tree and linkedlist with 1+ partitions, here we are going to use it for similar purpose.

Declaration - **(This code is also enclosed inside contracts{ } )**

//struct is keyword, age and name are variables

```
struct Person {
  uint age;
  string name;
}
```

### Chapter 6: Arrays

In languages like Cpp, Java and Python we have arrays or lists, which store elements in contigous memory allocations. In solidity also, we have arrays.

As in other languages, we have static(fixed size) and dynamic(variable sized) arrays, in solidity also, we have both types of arrays.

1. Declaration of static arrays-
 ```
 uint[2] fixedArray;
 // array can be of any data type, uint, int, string etc
 ```
 
2. Declaration of dynamic arrays-
 ```
uint[] dynamicArray;
 // array can be of any data type, uint, int, string etc
 ```

3. Declaration of struct arrays-
 ```
Person[] people; // dynamic Array, we can keep adding to it (kind of like a database)
 ```

4. **Public Arrays**

Solidity will automatically create a getter method( a function that returns a value ) for public array.

**Other contracts would then be able to read from, but not write to, this array. **

Declaration of public arrays-
 ```
Person[] public people;
//here Person is name os struct, public is keyword and people is name of public array

 ```
### Chapter 7: Function Declarations

 Syntax - 
 
 ```
 // name of function - eatHamburgers
 // parameters - string memory _name, uint _amount
 // 'function' - keyword ( in JS also, we declare function with 'function' keyword )
 // 'public' - function visibility
 
 function eatHamburgers(string memory _name, uint _amount) public {

}
 ```
 
 Function call - 
```
eatHamburgers("vitalik", 100);
 ```
 
It means that ** _name variable should be stored- in memory**. This is required for all reference types such as arrays, structs, mappings, and strings.

We have learnt about pass by value and pass by reference in languages like c++/java.

**By value**, which means that the Solidity compiler creates a new copy of the parameter's value and passes it to your function. This allows your function to modify the value without worrying that the value of the initial parameter gets changed.

**By reference**, which means that your function is called with a... reference to the original variable. Thus, if your function changes the value of the variable it receives, the value of the original variable gets changed.

#### NOTE - Start a function parameter variable names with an underscore (_) in order to differentiate them from global variables. 


### Chapter 8: Working With Structs and Arrays
```
// a structure Person, with age and name (resembles a real world person)
struct Person {
  uint age;
  string name;
}

//created a public array for the above defined structure
Person[] public people;
```

TASK - How to create new Persons and add them to our people array.

Step 1 - Create a new person
```
//Person PersonName = Person (70, "PersonName");
Person MIKIO = Person(20, "MIKIO");
// pass arguments carefully, age is first arg and name is second)
```

Step 2 - Add that person to the Array: (push, adds elements to the end of array)
``` 
//syntax of pushing in struct array is similar to vectors in cpp STL
people.push(MIKIO);
```

OR

SHORTHAND
```
people.push(Person(20, "SAKSHI"));
```

### Chapter 8: Private / Public Functions

In Solidity, functions are public by default. This means anyone (or any other contract) can call your contract's function and execute its code. As in lanugages like cpp and Java, we have access specifiers, public private protected, here we are introduced with public and private in solidity. Public functions can be called anywhere in the prgram, but private function can't be called, and are good for keeping data safe from attacks.

But we can mark functions as private by default, and then only make public the functions you want to expose to the world.

Syntax - 

```
//All we have to do is replace public keyword by private
uint[] numbers;   // variable of uint datatype

function _addToArray(uint _number) private {
  numbers.push(_number);      //pusing the parameter's value in numbers[]
}
```

### Chapter 10: More on Functions (return values)

Syntax-
```
string greeting = "What's up dog";

function sayHello() public returns (string memory) {
  return greeting;  // return type of greeting is string
}
```
The above function doesn't actually change state in Solidity — e.g. it doesn't change any values or write anything. (Only returns values)

So we could declare it as a **view function**, meaning **it's only viewing the data but not modifying it**

```
function sayHello() public view returns (string memory) {
```

Solidity also contains **pure functions**, which means you're not even accessing any data in the app. Consider the following:
```
function _multiply(uint a, uint b) private pure returns (uint) {
  return a * b;
}
```
This function doesn't even read from the state of the app — its return value depends only on its function parameters. So in this case we would declare the function as pure.

***In solididity we are defining the type of value func will return in its signature only***. In other languages we have a return type for function, but here we have to declare function with 'function' keyword only, and specify return type separately.

### Chapter 11: Keccak256 and Typecasting

Ethereum has the hash function **keccak256** built in, which is **a version of [SHA3](https://infosecwriteups.com/breaking-down-sha-3-algorithm-70fe25e125b6)**. A hash function basically maps an input into a random 256-bit hexadecimal number. A slight change in the input will cause a large change in the hash.

####  keccak256 expects a single parameter of type bytes. This means that we have to "pack" any parameters before calling keccak256

```
//6e91ec6b618bb462a4a6ee5aa2cb0e9cf30f7a052bb467b0ba58b8748c00d2e5
keccak256(abi.encodePacked("aaaab"));
```

As in other languages we do type casting, in solidity also, we need to cast a type into another sometimes, and this can be done without getting an error
Typecasting
```
uint8 a = 5;
uint b = 6;
// throws an error because a * b returns a uint, not uint8:
uint8 c = a * b;
// we have to typecast b as a uint8 to make it work:
uint8 c = a * uint8(b);
```

### Chapter 12: Events 

Events are a way for your contract to **communicate that something happened on the blockchain to your app front-end, which can be 'listening' for certain events and take action when they happen**.

Can say, its for interaction with front-end? Like our JS code does?!

```
// declare the event - it is declared before firing
event IntegersAdded(uint x, uint y, uint result);

function add(uint _x, uint _y) public returns (uint) {
  uint result = _x + _y;
  // fire an event to let the app know the function was called:
  emit IntegersAdded(_x, _y, result);
  return result;
}

```

JS Implementation
```
//A javascript implementation would look something like:

YourContract.IntegersAdded(function(error, result) {
})
```

## Chapter 14 - Web3.js - (javascript frontend that interacts with the contract)

#### Ethereum has a Javascript library called Web3.js.












