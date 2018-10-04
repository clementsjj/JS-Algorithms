# JS-Algorithms

Some Algorithm Practice with Javascript!

(Note: This is for Practice; All solutions should work, but may not be the best or most efficient)

- [String Algorithms](#string-algorithms)
  - [Reverse a String - No Methods]
  - [Find Longest Word in String]
  - [Replace and Capitalize]
  - [Evaluate String for Correct Pattern & return true/false](#evaluate-a-string)
  - [ABCheck - True if a and b are separated by exactly 3 places in a string](#abcheck)

---
### String Algorithms
#### Reverse a String - No Methods
```javascript
const str = "iliketoeat";
let temp;

const func = () => {
for (let i = str.length-1; i>=0; i--){
  temp += (str[i])
}
return temp
}
func();
```
---
#### Find Longest Word in String - Exclude Special Characters
Consists of two array for loops, one to replace irregular characters, and one to compare words to find the longest length
- Split the string by spaces into tempWords array
- Create longest word variable equal to ' '
- For loop through tempWords array replacing irregular characters with ''
  - This creates a new array called realArray that holds our testable words
- For loop through realArray comparing each index to thelongestword variable

```javascript
let word = "y.<>?'o bozo boy"
let tempWords;
let realArray = [];
let thelongestword = '';

const LongestWord = string => {
  tempWords = string.split(' ')

for(let i=0; i<tempWords.length; i++){
  realArray[i] = tempWords[i].replace(/\W/ig, '')
}

for (let i=0; i<realArray.length; i++){
  if (realArray[i].length > thelongestword.length){
    thelongestword = realArray[i];
  }
}
console.log("The Longest Word= ", thelongestword)
}

LongestWord(word)
```
More Concise Option:
```javascript
function longestword(str){
  let words = str.split(' ');
  var word ='';
  
  for (let i in words) {
    if (words[i].replace(/\W+/ig, '').length > word.length){
      word = words[i].replace(/\W+/ig, '');
    }
  }
  return word;
}
```
Even More Concise Option:
```javascript
return str.split(' ').map(word => word.replace(/[^a-zA-z]/g, '')).reduce((acc,value) => value.length > acc.length ? value : acc , ''))
```
---
#### Replace every letter in the string with the letter following it in the alphabet, and capitalize vowels
JJ Solution:
```javascript
let alphabet = ['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z'];
let vowels = ['a','e','i','o','u']

let testString = "i like the apples";
let regex = /[a-z]/ig

function LetterChanges(string) {
  let stringArray = string.split('');
  for (let i = 0; i<stringArray.length; i++){
    if(regex.test(stringArray[i]) === true){
        let alphIndex = alphabet.indexOf(string[i])
        stringArray[i] = alphabet[alphIndex+1]
    }
    if (vowels.includes(stringArray[i])){
      stringArray[i] = stringArray[i].toUpperCase();
    }
  }
  let newString = stringArray.join('')
  console.log(newString)
}

LetterChanges(testString)
```

Pak Solution:
- Uses alphabet.indexOf(str[i]), Returns -1 if it is not present, which allows you to skip spaces and non alphabet characters
```javascript
const Changes = (str) => {
  let alphabet = 'abcdefghijklmnopqrstuvwxyza';
  let result = '';
  
  for (let i=0; i<str.length; i++){
    if (alphabet.indexOf(str[i]) >= 0) {
      let foundAlphabetIndex = alphabet.indexOf(str[i]);
      result += alphabet[foundAlphabetIndex + 1];
    } else{
      result += str[i];
    }
  }
  return result.replace(/a|e|i|o|u/g, function(c){
    return c.toUpperCase();
  })
}
Changes("hey man");
```
---
#### Evaluate a String 
All a-z chars must be =f= or +f+ for the string to be true. Else=false;
Example: 

==+f+===r==+  --> True

===f+==y=     --> False

JJ Solution:
```javascript
function SimplySymbol(string) {
  let tempArray = string.split('')
  let re =  /[a-z]/ig
  let isTrue = false;
  console.log(tempArray)

for (let i=0; i<tempArray.length; i++){
  console.log('Test: ', tempArray[i])
if(re.test(tempArray[i])==true){
  console.log('Enter Loop With: ', tempArray[i])
  if( (tempArray[i-1] == '=' && tempArray[i+1] =='=') || (tempArray[i-1] == '+' && tempArray[i+1] =='+') ){
    console.log("Passes Test. isTrue=true")
    isTrue = true;
  } else return false
} //End Big If
} //End For Loop
  return isTrue;
} //End Function

testStr = '===s=+a+===+d+'
SimplySymbol(testStr);
```
Dwyer Solution:
```javascript
function SimplySymbol(str) {
 var patt = /[a-z]/gi
 let a = 0;
 let b = 0;
 for (let i = 0; i < str.length; i++) {
   if( patt.test(str[i]) ) {
     a++
     if(str[i-1] == str[i+1]) {
       b++
   }};
 };
 if ( a == b) {
   return true;
 } else {
   return false;
 }
}

console.log(SimplySymbol(‘===s=+a+++++d+‘));
console.log(‘-------‘);
console.log(SimplySymbol(‘===d===c+++a+‘));
console.log(‘-------’);
```
Pak Solution:
```javascript
function SimpleSymbols(str) { 

    let indexes = [];
    let counter = 0;
    let plusCount = 0;
    let equalCount = 0
  
    for(let i = 0; i < str.length; i++) {
      if (str[i].search(/[^A-Za-z0-9]+/g)) {
        counter++;
        indexes.push(i)
      }
    } 
    for(let j = 0; j < indexes.length; j++) {
      if (str[indexes[j] - 1] === '+' && str[indexes[j] + 1] === '+') {
       plusCount++;
      } else if (str[indexes[j] - 1] === '=' && str[indexes[j] + 1] === '=') {
        equalCount++
      }
    }
    if ( (plusCount + equalCount) === counter) {
      return true;
    } else {
      return false;
    }
}
module.exports = SimpleSymbols;
```
---
#### ABCheck 
- True if a and b are separated by exactly 3 places in a string
JJ Solution:

Only checks the first 'a' and 'b'
```javascript
function abcheck(s) {
str = s.toLowerCase();
let indexA;
let indexB;

for (let i=0; i < str.length; i++){
  if(str[i].charCodeAt() == 97 && indexA == undefined ){
    indexA=str.indexOf(str[i])
  }
  if(str[i].charCodeAt() == 98 && indexB == undefined){
    indexB=str.indexOf(str[i])
  }
}

if((indexA - indexB) == 4 || indexB - indexA == 4){
  return true
}else return false
}
var string = "Lane borrowed"
abcheck(string)
```

Solution 2:

~~...But gets undefined evaluating str[i-4] in stringToo :(  ...~~
If str[i+4] or [i-4] is undefined as a character, thats fine. The functin can return false The program will crash, however, if you try to run a method, like charCodeAt() on an undefined value. 

In this case, it may be better to evaluate the string itself, like `str[i-4] === 'b'` instead of the charCode.

charCodeAt() is still cool though.

```javascript
function abcheckTwo(s) {
str = s.toLowerCase();

for (let i=0; i < str.length; i++){
  if(str[i].charCodeAt() == 97){
    if(str[i+4].charCodeAt()==98 || str[i-4].charCodeAt()==98) { 
      return true;
    }//End If 2
  }//End If 1
}//End For Loop
  return false //default if no condition is met
} //end function abcheckTwo

var stringOne='lane borrowed'
var stringToo='laneb borrowed'
abcheckTwo(stringOne)
```
