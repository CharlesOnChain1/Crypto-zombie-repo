# CryptoZombie

---
## Hello World 

Create a empty contract ZombieFactory(殭屍工廠) used version of solidity 0.4.25

``` solidity=
pragama ^0.4.25; 

contract ZombieFactory{
    // test 
}
```
---

## Zombie DNA

Our Zombie DNA is going to be determined by a 16-digit number.
Declare a uint named dnaDigits, and set it equal to 16.

``` solidity=
pragama ^0.4.25; 

contract ZombieFactory{
    uint dnaDigits = 16; // set zombie DNA 
}
```

---

## Math Operations 

- Addition: x + y
- Subtraction: x - y
- Multiplication: x * y
- Division: x / y
- Modulus / remainder: x % y (for example, 13 % 5 is 3, because if you divide 5 into 13, 3 is the remainder)

``` solidity=
uint x = 5 ** 2; // equal to 5^2 = 25
```
To make sure our Zombie's DNA is only 16 characters, let's make another uint equal to 10^16. That way we can later use the modulus operator % to shorten an integer to 16 digits.
- Create a uint named dnaModulus, and set it equal to 10 to the power of dnaDigits.

``` solidity=
pragama ^0.4.25; 

contract ZombieFactory{
    uint dnaDigits = 16; // set zombie DNA 
    uint dnaModulus = 10 ** dnaDigits;
}
```

---
## Structs 
Sometimes you need a more complex data type. For this, Solidity provides structs:

``` solidity= 
struct Person {
  uint age;
  string name;
}
```

In our app, we're going to want to create some zombies! And zombies will have multiple properties, so this is a perfect use case for a struct.

- Create a struct named Zombie.
- Our Zombie struct will have 2 properties: name (a string), and dna (a uint).

``` solidity=
pragma solidity ^0.4.25;

contract ZombieFactory {

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;
    
    struct Zombie{
        string name;
        uint dna;
    }
}
```

---
## Arrays 
When you want a collection of something, you can use an array. 
``` solidity=
// Array with a fixed length of 2 elements:
uint[2] fixedArray;

// another fixed Array, can contain 5 strings:
string[5] stringArray;

// a dynamic Array - has no fixed size, can keep growing:
uint[] dynamicArray;

Person[] people; // dynamic Array, we can keep adding to it

Person[] public people;
// Public Array

```
We're going to want to store an army of zombies in our app. 

``` solidity=
pragma solidity ^0.4.25;

contract ZombieFactory {

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;

    struct Zombie {
        string name;
        uint dna;
    }

    Zombie[] public zombies; 
    // Zombie is a struct and we will put zombies to it .
}
```

---
## Function Declarations

example 
``` solidity= 
function eatHamburgers(string _name, uint _amount) {
}
```
You will call function like 
``` solidity=
eatHamburgers("vitalik", 100);
```
In our app, we're going to need to be able to create some zombies. Let's create a function for that.
- Create a function named createZombie. It should take two parameters: _name (a string), and _dna (a uint).

``` solidity=
pragma solidity ^0.4.25;

contract ZombieFactory {

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;

    struct Zombie {
        string name;
        uint dna;
    }

    Zombie[] public zombies;

    function createZombie(string _name,uint _dna){
        
    }
}
```

---
## Working With Structs and Arrays
previous our struct 
``` solidity=
struct Person {
  uint age;
  string name;
}
Person[] public people;
```
Create a new struct and add them to our array
``` solidity=
// create a New Person:
Person satoshi = Person(172, "Satoshi");

// Add that person to the Array:
people.push(satoshi);
```

We can combine these together and do them in one line of code to keep it clean .
```  solidity=
people.push(Person(16, "Vitalik"));
``` 
Let's make our createZombie function do something!

- Fill in the function body so it creates a new Zombie, and adds it to the zombies array. 
- The name and dna for the new Zombie should come from the function arguments.
- Let's do it in one line of code to keep things clean.
``` solidity=
pragma solidity ^0.4.25;

contract ZombieFactory {

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;

    struct Zombie {
        string name;
        uint dna;
    }

    Zombie[] public zombies;

    function createZombie (string _name, uint _dna) {
        zombies.push(Zombie(_name, _dna));
    }

}
```

---
private and public function 
- In Solidity, functions are public by default.
- example : 
``` solidity=
uint[] numbers;

function _addToArray(uint _number) private {
  numbers.push(_number);
}
```
public to private , private function name will add _ and private .

``` solidity= 
pragma solidity ^0.4.19;

contract ZombieFactory {

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;

    struct Zombie {
        string name;
        uint dna;
    }

    Zombie[] public zombies;

    function _createZombie(string _name, uint _dna) private {
        zombies.push(Zombie(_name, _dna));
    }

}
```

---
## More on function 
we're going to learn about Function return values, and function modifiers.

### Return Values 
``` solidity=
string greeting = "What's up dog";

function sayHello() public returns (string) {
  return greeting;
}
``` 

### function modifiers 
``` solidity=
function sayHello() public view returns (string) {

function _multiply(uint a, uint b) private pure returns (uint) {
  return a * b;
}
``` 

We're going to want a helper function that generates a random DNA number from a string.

- Create a private function called _generateRandomDna. It will take one parameter named _str (a string), and return a uint.

- This function will view some of our contract's variables but not modify them, so mark it as view.

- The function body should be empty at this point — we'll fill it in later.

``` solidity=
pragma solidity ^0.4.25;

contract ZombieFactory {

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;

    struct Zombie {
        string name;
        uint dna;
    }

    Zombie[] public zombies;

    function _createZombie(string _name, uint _dna) private {
        zombies.push(Zombie(_name, _dna));
    }

    function _generateRandomDna(string _str) private view returns (uint){
        
    }

}
```

---
Ethereum has the hash function keccak256 built in, which is a version of SHA3 convert to 256-bit hexidecimal number. 
``` solidity=
keccak256(abi.encodePacked("aaaab"));
```

Typecasting 
``` solidity=
uint8 a = 5;
uint b = 6;
// throws an error because a * b returns a uint, not uint8:
uint8 c = a * b; 
// we have to typecast b as a uint8 to make it work:
uint8 c = a * uint8(b); 
```
_generateRandomDna
``` solidity=
pragma solidity ^0.4.25;

contract ZombieFactory {

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;

    struct Zombie {
        string name;
        uint dna;
    }

    Zombie[] public zombies;

    function _createZombie(string _name, uint _dna) private {
        zombies.push(Zombie(_name, _dna));
    } 

    function _generateRandomDna(string _str) private view returns (uint) {
        uint rand = uint(keccak256(abi.encodePacked(_str)));
        return rand % dnaModulus;
    }

}
```

---
## Putting It Together

``` solidity=
pragma solidity ^0.4.25;

contract ZombieFactory {

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;

    struct Zombie {
        string name;
        uint dna;
    }

    Zombie[] public zombies;

    function _createZombie(string _name, uint _dna) private {
        zombies.push(Zombie(_name, _dna));
    } 

    function _generateRandomDna(string _str) private view returns (uint) {
        uint rand = uint(keccak256(abi.encodePacked(_str)));
        return rand % dnaModulus;
    }

    function createRandomZombie(string _name) public{
        uint randDna = _generateRandomDna(_name);
        _createZombie(_name, randDna);
    }

}
```

---
## Events
Our contract is almost finished! Now let's add an event.

Events are a way for your contract to communicate that something happened on the blockchain to your app front-end, which can be 'listening' for certain events and take action when they happen.

Example:
``` solidity=
// declare the event
event IntegersAdded(uint x, uint y, uint result);

function add(uint _x, uint _y) public {
  uint result = _x + _y;
  // fire an event to let the app know the function was called:
  emit IntegersAdded(_x, _y, result);
  return result;
}
```

``` javascript=
YourContract.IntegersAdded(function(error, result) { 
  // do something with result
}
```

We want an event to let our front-end know every time a new zombie was created, so the app can display it.

Declare an event called NewZombie. It should pass zombieId (a uint), name (a string), and dna (a uint).

Modify the _createZombie function to fire the NewZombie event after adding the new Zombie to our zombies array.

You're going to need the zombie's id. array.push() returns a uint of the new length of the array - and since the first item in an array has index 0, array.push() - 1 will be the index of the zombie we just added. Store the result of zombies.push() - 1 in a uint called id, so you can use this in the NewZombie event in the next line.

``` solidity=
pragma solidity ^0.4.25;

contract ZombieFactory {

    event NewZombie(uint zombieId, string name, uint dna);

    uint dnaDigits = 16;
    uint dnaModulus = 10 ** dnaDigits;

    struct Zombie {
        string name;
        uint dna;
    }

    Zombie[] public zombies;

    function _createZombie(string _name, uint _dna) private {
        uint id = zombies.push(Zombie(_name, _dna)) -1 ;
        emit NewZombie(id, _name, _dna);
    } 

    function _generateRandomDna(string _str) private view returns (uint) {
        uint rand = uint(keccak256(abi.encodePacked(_str)));
        return rand % dnaModulus;
    }

    function createRandomZombie(string _name) public {
        uint randDna = _generateRandomDna(_name);
        _createZombie(_name, randDna);
    }

}
```

---
## Web3.js
Zombie touch our contract
``` javascript=
// Here's how we would access our contract:
var abi = /* abi generated by the compiler */
var ZombieFactoryContract = web3.eth.contract(abi)
var contractAddress = /* our contract address on Ethereum after deploying */
var ZombieFactory = ZombieFactoryContract.at(contractAddress)
// `ZombieFactory` has access to our contract's public functions and events

// some sort of event listener to take the text input:
$("#ourButton").click(function(e) {
  var name = $("#nameInput").val()
  // Call our contract's `createRandomZombie` function:
  ZombieFactory.createRandomZombie(name)
})

// Listen for the `NewZombie` event, and update the UI
var event = ZombieFactory.NewZombie(function(error, result) {
  if (error) return
  generateZombie(result.zombieId, result.name, result.dna)
})

// take the Zombie dna, and update our image
function generateZombie(id, name, dna) {
  let dnaStr = String(dna)
  // pad DNA with leading zeroes if it's less than 16 characters
  while (dnaStr.length < 16)
    dnaStr = "0" + dnaStr

  let zombieDetails = {
    // first 2 digits make up the head. We have 7 possible heads, so % 7
    // to get a number 0 - 6, then add 1 to make it 1 - 7. Then we have 7
    // image files named "head1.png" through "head7.png" we load based on
    // this number:
    headChoice: dnaStr.substring(0, 2) % 7 + 1,
    // 2nd 2 digits make up the eyes, 11 variations:
    eyeChoice: dnaStr.substring(2, 4) % 11 + 1,
    // 6 variations of shirts:
    shirtChoice: dnaStr.substring(4, 6) % 6 + 1,
    // last 6 digits control color. Updated using CSS filter: hue-rotate
    // which has 360 degrees:
    skinColorChoice: parseInt(dnaStr.substring(6, 8) / 100 * 360),
    eyeColorChoice: parseInt(dnaStr.substring(8, 10) / 100 * 360),
    clothesColorChoice: parseInt(dnaStr.substring(10, 12) / 100 * 360),
    zombieName: name,
    zombieDescription: "A Level 1 CryptoZombie",
  }
  return zombieDetails
}
```

###### tags: `dapp` `cryptozombie` `blockchain`