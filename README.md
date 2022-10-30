# CCauthenticator
Project from Codecademy Back End Developer Program

## These arrays were all provided by Codecademy
**// All valid credit card numbers** \
const valid1 = [4, 5, 3, 9, 6, 7, 7, 9, 0, 8, 0, 1, 6, 8, 0, 8]; \
const valid2 = [5, 5, 3, 5, 7, 6, 6, 7, 6, 8, 7, 5, 1, 4, 3, 9]; \
const valid3 = [3, 7, 1, 6, 1, 2, 0, 1, 9, 9, 8, 5, 2, 3, 6]; \
const valid4 = [6, 0, 1, 1, 1, 4, 4, 3, 4, 0, 6, 8, 2, 9, 0, 5]; \
const valid5 = [4, 5, 3, 9, 4, 0, 4, 9, 6, 7, 8, 6, 9, 6, 6, 6]; 

**// All invalid credit card numbers** \
const invalid1 = [4, 5, 3, 2, 7, 7, 8, 7, 7, 1, 0, 9, 1, 7, 9, 5]; \
const invalid2 = [5, 7, 9, 5, 5, 9, 3, 3, 9, 2, 1, 3, 4, 6, 4, 3]; \
const invalid3 = [3, 7, 5, 7, 9, 6, 0, 8, 4, 4, 5, 9, 9, 1, 4]; \
const invalid4 = [6, 0, 1, 1, 1, 2, 7, 9, 6, 1, 7, 7, 7, 9, 3, 5]; \
const invalid5 = [5, 3, 8, 2, 0, 1, 9, 7, 7, 2, 8, 8, 3, 8, 5, 4];

**// Can be either valid or invalid** \
const mystery1 = [3, 4, 4, 8, 0, 1, 9, 6, 8, 3, 0, 5, 4, 1, 4]; \
const mystery2 = [5, 4, 6, 6, 1, 0, 0, 8, 6, 1, 6, 2, 0, 2, 3, 9]; \
const mystery3 = [6, 0, 1, 1, 3, 7, 7, 0, 2, 0, 9, 6, 2, 6, 5, 6, 2, 0, 3]; \
const mystery4 = [4, 9, 2, 9, 8, 7, 7, 1, 6, 9, 2, 1, 7, 0, 9, 3]; \
const mystery5 = [4, 9, 1, 3, 5, 4, 0, 4, 6, 3, 0, 7, 2, 5, 2, 3];

**// An array of all the arrays above** \
const batch = [valid1, valid2, valid3, valid4, valid5, invalid1, invalid2, invalid3, invalid4, invalid5, mystery1, mystery2, mystery3, mystery4, mystery5];

## The following code is all mine

This first function reverses the arrays provided by codecademy containing the card numbers to take advantage of the Luhn algorithm. The Luhn algorithm looks at the digits from a CC to determine if a CC is valid or invalid.

### A general outline of the step one: ### 
A scenario was given that you are and other employees are tasked with determining whether a number of credit cards were valid or invalid. The other employees were using old fashioned pencil and paper to determine if the cards are legitimate, using the Luhn algorithm. As an aspiring developer, you are determined to use the power of computers to be able to quickly process many CC at once.
1. Create the validateCred arrow function that accepts a single 'arr' as a parameter.
2. Create an empty 'reverseArr' to hold the values of the 'arr' in reverse.
3. Use a For loop to start at the end of the inserted 'arr' and to push those results into the empty 'reverseArr'.
4. Create an empty luhnArr.
5. Use a for loop to go from the start of the 'reverseArr' to the end, using if, else if, and else to determine what sort of math should be performed on the CC numbers and push those to the 'luhnArr'. For a better explanation of the Luhn algorithm, [click here](https://en.wikipedia.org/wiki/Luhn_algorithm#Description).
6. Sum the altered luhnArr and then determine if the number is perfectly divisible by 10. If so, you have a valid CC! \ 
   ``` 
   const validateCred = arr =>{
      let reverseArr = [];
      for (let i=arr.length-1; i>=0; i--){
        reverseArr.push(arr[i]);
      }
      let luhnArr = [];
      for (let k=0; k<reverseArr.length; k++){
        let num = reverseArr[k];
        if(k % 2 !== 0 && num*2 > 9){
          luhnArr.push((num*2) - 9);
        }
        else if(k % 2 !== 0){
          luhnArr.push(num*2);
        }
        else{
          luhnArr.push(num);
        }
      }
      function sum_reducer(accumulator, currentValue) {
      return accumulator + currentValue;
      }
      let sum = luhnArr.reduce(sum_reducer);
      //return sum
      if(sum%10 == 0){
        return true;
      } else {
        return false;
      }
    } 
    ```

**//This console.log helps verify that a card is valid**

```
console.log(validateCred(valid5));
```

### A general outline of step two: ###
Next, we wanted to be able to take a batch of cards and determine which cards were valid and which were invalid, and push them into new arrays. The 'batch' arr provided by Codecademy was helpful for this.
1. First, I created two empty arr. One to accept all invalid cards, and a second to accept all valid cards.
2. Then I created an arrow function that accepted a single arr as a parameter.
3. I used a for loop to go through the inserted arr parameter. 
4. I used an if function to determine if the elements within the arr parameter returned true or false values in the validateCred function I previously created. 
5. I pushed 'true' values to the valid card arr and 'false' values to the invalid card arr.
6. To fill the allInvalidCardArr and allValidCardArr, the function is then called on the 'batch' arr.
7. The console.log(allValidCardArr) and console.log(allInvalidCardArr) were used to check the results.

```
let allInvalidCardArr = [];
let allValidCardArr = [];

const findInvalidCards = arr =>{
    for (let i=0; i<arr.length; i++){
      validateCred(arr[i]);
    if (validateCred(arr[i]) === false){
      allInvalidCardArr.push(arr[i]);
    } else {
      allValidCardArr.push(arr[i]);
    }
  }  
}

findInvalidCards(batch);

console.log(allValidCardArr);
console.log(allInvalidCardArr);
```

### A general outline of step three: ###
Now that I could determine which cards were invalid, I wanted to be able to reach out to the issuing companies and let them know the cards that had been issued using invalid numbers. It was important that regardless of the number of invalid cards a company issued, we only wanted the company name to appear once on the list.
1. First, I made an empty arr called callTheseCardCo.
2. Then I created an empty arrow function that accepted a single arr as a parameter.
3. Within the function, I created an empty invalidCardCompanies arr. This would accept **all** of the invalid companies. This arr had duplicates.
4. Used a for loop to check the first element of each nested arr to find the first digit of each card. \
3 - AMEX, 4 - Visa, 5 - Mastercard, 6 - Discover.
5. Finally, used indexOf on the invalidCardCompanies arr to push the first occurance of the four companies to the empty callTheseCardCo arr.
6. Called the idInvalidCardCompanies on the allInvalidCardArr.
7. Used the console.log(callTheseCardCo) to view the list of companies that needed called.

```
let callTheseCardCo = [];

const idInvalidCardCompanies = arr =>{
  let invalidCardCompanies = [];
  for (let i =0; i<arr.length; i++){
    let cardCo = arr[i][0];
    if(cardCo==3){
      invalidCardCompanies.push('Amex')
    } else if (cardCo==4){
      invalidCardCompanies.push('Visa')
    } else if (cardCo==5){
      invalidCardCompanies.push('Mastercard')
    } else if (cardCo==6){
      invalidCardCompanies.push('Discover')
    } else {
      invalidCardCompanies.push('Company not found')
    }
  }
  if (invalidCardCompanies.indexOf('Visa')>=0){
    callTheseCardCo.push('Visa')
  }
  if (invalidCardCompanies.indexOf('Mastercard')>=0){
    callTheseCardCo.push('Mastercard')
  }
  if (invalidCardCompanies.indexOf('Amex')>=0){
    callTheseCardCo.push('Amex')
  }
  if (invalidCardCompanies.indexOf('Discover')>=0){
    callTheseCardCo.push('Discover')
  }
}

idInvalidCardCompanies(allInvalidCardArr);
console.log(callTheseCardCo);
```

Because I am nuts about double checking, I commented out all cards issued by AMEX (first digit 3) just to see if the functions were working properly. When I did that, only Visa, Mastercard, and Discover were returned in the callTheseCardCo arr.
