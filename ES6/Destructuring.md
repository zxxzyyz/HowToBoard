### Destructuring
Basic Examples
```Javascript
const wes = {
  first: 'Wes',
  last: 'Bos',
  links: {
    social: {
      twitter: 'https://twitter.com/wesbos',
      facebook: 'https://facebook.com/wesbos.developer',
    },
    web: {
      blog: 'https://wesbos.com'
    }
  }
};

const { twitter: tweet, facebook: fb } = wes.links.social;

const settings = { width: 300, color: 'black' }
const { width = 100, height = 100, color = 'blue', fontSize = 25} = settings;
```
Example for Objects
```Javascript
const { w: width = 400, h: height = 500 } = { w: 800 }
```
Example for Arrays
```Javascript
const details = ['Wes Bos', 123, 'wesbos.com'];
const [name, id, website] = details;
console.log(name, id, website);

const data = 'Basketball,Sports,90210,23,wes,bos,cool';
const [itemName, category, sku, inventory] = data.split(',');

const team = ['Wes', 'Harry', 'Sarah', 'Keegan', 'Riker'];

const [captain, assistant, ...players] = team;
```
Example for Real World
```Javascript
let inRing = "Hulk Hogan";
let onSide = "The Rock";
[inRing, onSide] = [onSide, inRing];
```
Examples for Functions
```Javascript
// 1st Example
function convertCurrency(amount) {
  const converted = {
    USD: amount * 0.76,
    GPB: amount * 0.53,
    AUD: amount * 1.01,
    MEX: amount * 13.30
  };
  return converted;
}
const { AUD, USD } = convertCurrency(100);
// 2nd Example
function tipCalc({total = 100, tip = 0.15, tax = 0.13} = {}) {
  return total + (tip * total) + (tax * total);
}
const bill = tipCalc();
console.log(bill);
```