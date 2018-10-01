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
### Find Longest Word in String - Exclude Special Characters
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

console.log("TempWords= ", tempWords)
console.log("RealArray= ", realArray);


  for (let i=0; i<realArray.length; i++){
    if (realArray[i].length > thelongestword.length){
      thelongestword = realArray[i];
    }
  }

  console.log("The Longest Word= ", thelongestword)
}

LongestWord(word)
```
