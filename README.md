# JS-Algorithms

Some Algorithm Practice with Javascript!
(Note: This is for Practice)

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
