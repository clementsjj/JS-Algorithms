# JS-Algorithms

Some Algorithm Practice with Javascript!

(Note: This is for Practice; All solutions should work, but may not be the best or most efficient)

- [String Algorithms](#string-algorithms)
  - [Reverse a String - No Methods]
  - [Find Longest Word in String]
  - [Replace and Capitalize]

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
