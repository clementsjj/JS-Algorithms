# JS-Algorithms

Some Algorithm Practice with Javascript!

(Note: This is for Practice; All solutions should work, but may not be the best or most efficient)

- [String Algorithms](#string-algorithms)
  - [Reverse a String - No Methods](#string-algorithms)
  - [Find Longest Word in String]
  - [Replace and Capitalize]
  - [Evaluate String for Correct Pattern & return true/false](#evaluate-a-string)
  - [ABCheck - True if a and b are separated by exactly 3 places in a string](#abcheck)
  - [Arithmetic or Geometric](#arithmetic-or-geometric)
  - [Array-Index Value Equals Product of Other Array Values](#index-product)
  - [Add '-' (dash) Between Odd Numbers](#add-dash-between-odds)
  - [Add numbers hidden in a string](#number-addition)

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
Pak Solution:
```javascript
function abCheck(str) {
  str = str.toLowerCase();
  var counter = 0;

  for (let i = 0; i < str.length; i++) {
    if (str[i].charCodeAt() === 97) {
      if (str[i + 4] === 'b' || str[i - 4] === 'b') {
        counter += 1;
      }
    } else if (str[i].charCodeAt() === 98) {
       if (str[i + 4] === 'a' || str[i - 4] === 'a') {
        counter += 1;
      }
    }
  }

  if (counter > 0) {
    return 'true';
  } else {
    return 'false';
  }
}
```
---
#### Arithmetic or Geometric
- If values in an array change by addition or subtractin, then Arithmetic
- If values in an array change by muiltiplication or division, then Geometric

JJ Solution
- Manual check for first 3 variables. NOT ideal solution, since it depends on evaluating the first 3 values instead of a loop
- Only checks addition and multiplication or none
```javascript
function ArithGeo(arr) {
  let mathThing;
  let arthSeq = false;
  let geoSeq = false;
  let nonSeq = false;

  let a = arr[0];
  let b = arr[1];
  let c = arr[2];
  if (a!==undefined && b !== undefined && c !== undefined){ 
    //should also check for zero and negative number

    //check addition & subtraction
    mathThing = b - a;
    console.log('mathThing= ', mathThing)
    if ((c-b) === mathThing){
      //If we are here, things are good. One last check...
      if(arr[3] !== undefined){
        if((c + mathThing) == arr[3]){
          arthSeq = true;
          return 'Arithmetic'
        }else {
          arthSeq = false;
        }
      }else {
        arthSeq = true;
        console.log('There is no 4th index');
      }
    }

    //check mult and div
    mathThing = b/a
    if((b*mathThing) == c){
      //If we are here, things are good. One last check...
      if(arr[3] !== undefined){
        if((c*mathThing)===arr[3]){
          geoSeq = true;
          return "Geometric";
        } else {
          GeoSeq = false;
        }
      }else{
        geoSeq = true;
        console.log("There is no 4th index");
      }
    }
}//End if NOT undefined
if (arthSeq!==true && geoSeq!==true){
  nonSeq = true;
  return -1;
}

if(arthSeq == true){return "Arithmeticy"}
if(geoSeq == true){ return "Geometricy"}
if(nonSeq == true){return -11}
} //Function

let arthArry = [2, 4, 6, 8]
let geoArry = [2,6,18,54]
let nonArry = [1,20,55]

ArithGeo(arthArry);
//ArithGeo(geoArry)
//ArithGeo(nonArry)
```
Pak Solution:
- Uses a tester
```javascript
function patternDetect(arr) {
    // var arith, geo;
    // for (let i = 0; i < arr.length; i++) {
    //     arith = arr[arr.length - 1] - arr[arr.length - 2];
    //     geo = arr[arr.length - 1] / arr[arr.length - 2];
    //     if (arr[i] + arith === arr[i + 1]) {
    //         return 'Arithmetic';
    //     } else if (arr[i] * geo === arr[i + 1]) {
    //         return 'Geometric';
    //     } else {
    //         return -1;
    //     }
    // }
    if (pattern[3] - pattern[2] === pattern[2] - pattern[1] && pattern[2] - pattern[1] === pattern[1] - pattern[0]) {
        return "Arithmetic";
    } else if (pattern[3] / pattern[2] === pattern[2] / pattern[1] && pattern[2] / pattern[1] === pattern[1] / pattern[0]) {
        return "Geometric";
    } else return -1;
}
// patternDetect([2, 4, 6, 8]);
console.log(patternDetect([100, 50, 25, 12.5]));
module.exports = patternDetect;
```
---
#### Index Product
-  A value at index of an array equals product of all other values in the array.
- [1,4,3] should return [12,3,4]

Pak Solution:
```javascript
function otherProducts(arr) {
 let results = [];
 for (let i = 0 ; i < arr.length; i++) {
     let tempValue = 0;
     let accuValue = 1;
   for (let j = 0; j < arr.length; j++) {
     if ( i === j) {
       continue;
     }
     tempValue = arr[j];
     accuValue = tempValue * accuValue;
   }
   results.push(accuValue);
 }
 return results;
}
otherProducts([1, 4, 3]);
```
---
#### Add Dash Between Odds
- Add a '-' (dash) between two odd numbers in a string

Pak Solution: 
```javascript
function DashInsert(str) {

 let i, array = [], result = "";

 for ( i = 0; i < str.length; i++ ) {
   array.push(parseInt(str[i]));
 }

 for (i = 0; i < array.length; i++) {
   if (array[i] % 2 !== 0 && array[i+1] % 2 !== 0) {
     result += array[i];
     result += '-';
   } else {
     result += array[i];
   }
 }

 var finalAnswer;

 if (result[result.length-1] === '-') {
   finalAnswer = result.slice(0, [result.length-1]);
   return finalAnswer;
 } else {
   return result;
 }
}
DashInsert('454793');
```
#### Number Addition
- Take a string such as "55Hello 6" and add numbers together (i.e. 61). 
- Be sure numbers like 55 are together as one number

Pak Solution:
```javascript
function NumberAddition(str) {
 let digits = '0123456789';
 let numbers = [];
 let numberString = '';

 for (let i = 0; i < str.length; i++) {
   if (!digits.includes(str[i])) {
     if (numberString !== '') {
       numbers.push(numberString);
     }
     numberString = '';
   } else {
     numberString += str[i];
     if ( i === str.length - 1) {
       numbers.push(numberString)
     }
   }
 }
 let sum = 0;
 for (let i = 0; i < numbers.length; i++) {
   sum += parseInt(numbers[i]);
 }
 return sum;
}
NumberAddition('6hello 65')
```
