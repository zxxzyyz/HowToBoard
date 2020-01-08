# Concepts of ES6

### Let and Const
```
EZ
```
### Arrow Function
When you really need `this`
```Javascript
const button = document.querySelector("#pushy");
button.addEventListener("click", function() {
  console.log(this);
  this.classList.toggle("on");
});
```
When you need a method to bind to an object
```Javascript
const person = {
  points: 23,
  score() {
    console.log(this);
    this.points++;
  }
};
```
When you need to add a prototype method
```Javascript
class Car {
  constructor(make, colour) {
    this.make = make;
    this.colour = colour;
  }
}

const beemer = new Car("bmw", "blue");
const subie = new Car("Subaru", "white");

Car.prototype.summarize = function() {
  return `This car is a ${this.make} in the colour ${this.colour}`;
};
```
When you need arguments object
```Javascript
const orderChildren = function() {
  const children = Array.from(arguments);
  console.log(children);
  return children.map((child, i) => {
    return `${child} was child #${i + 1}`;
  });
  console.log(arguments);
};
```
All other cases
```Javascript
<li data-time="5:17">Flexbox Video</li><li data-time="8:22">Flexbox Video</li><li data-time="3:34">Redux Video</li>
<li data-time="5:23">Flexbox Video</li><li data-time="7:12">Flexbox Video</li><li data-time="7:24">Redux Video</li>
<li data-time="6:46">Flexbox Video</li><li data-time="4:45">Flexbox Video</li><li data-time="4:40">Flexbox Video</li>
<li data-time="7:58">Redux Video</li><li data-time="11:51">Flexbox Video</li><li data-time="9:13">Flexbox Video</li>
<li data-time="5:50">Flexbox Video</li><li data-time="5:52">Redux Video</li><li data-time="5:49">Flexbox Video</li>
<li data-time="8:57">Flexbox Video</li><li data-time="11:29">Flexbox Video</li><li data-time="3:07">Flexbox Video</li>

const items = Array.from(document.querySelectorAll('[data-time]'));

// Filter for only the elements that contain the word 'Flexbox'
const filtered = items
  .filter(item => item.textContent.includes('Flexbox'))
  // map down to a list of time strings
  .map(item => item.dataset.time)
  // map to an array of seconds
  .map(timecode => {
    const parts = timecode.split(':').map(part => parseFloat(part));
    return (parts[0] * 60) + parts[1];
  })
  // reduce to get total
  .reduce((runningTotal, seconds) => runningTotal + seconds);

console.log(filtered);
```
### Template Strings
Example 1
```Javascript
const dict = {
  HTML: 'Hyper Text Markup Language',
  CSS: 'Cascading Style Sheets',
  JS: 'JavaScript'
};

function addAbbreviations(strings, ...values) {
  const abbreviated = values.map(value => {
    if(dict[value]) {
      return `<abbr title="${dict[value]}">${value}</abbr>`
    }
    return value;
  });

  return strings.reduce((sentence, string, i) => {
    return sentence + string + (abbreviated[i] || '');
  }, '');
}

const first = 'Wes';
const last = 'Bos';
const sentence = addAbbreviations`Hi my name is ${first} ${last} and I love to code ${'JS'}, ${'HTML'} and ${'CSS'} all day and all night long!`
```
Example 2
```Javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/dompurify/0.8.2/purify.min.js"></script>
<script>
  function sanitize(strings, ...values) {
    const dirty = strings.reduce((prev, next, i) => `${prev}${next}${values[i] || ''}`, '');
    return DOMPurify.sanitize(dirty);
  }

  const first = 'Wes';
  const aboutMe = `I love to do evil <img src="http://unsplash.it/100/100?random" onload="alert('you got hacked');" />`;

  const html = sanitize`<h3>${first}</h3><p>${aboutMe}</p>`;
  document.body.innerHTML = html;
</script>
```
Example 3
```Javascript
const beer = {
  name: 'Belgian Wit',
  brewery: 'Steam Whistle Brewery',
  keywords: ['pale', 'cloudy', 'spiced', 'crisp']
};

function renderKeywords(keywords) {
  return `
    <ul>
      ${keywords.map(keyword => `<li>${keyword}</li>`).join('')}
    </ul>
  `;
}

const markup = `
  <div class="beer">
    <h2>${beer.name}</h2>
    <p class="brewery">${beer.brewery}</p>
    ${renderKeywords(beer.keywords)}
  </div>
`;

document.body.innerHTML = markup;
```
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
### For Loop And Arrays
```Javascript
/* eslint-disable */
Array.prototype.shuffle = function() {
  let i = this.length, j;
  if (i == 0) return this;
  while (--i) {
    j = Math.floor(Math.random() * (i + 1));
    [i, j] = [j, i];
  }
  return this;
}

const cuts = ["Chuck", "Brisket", "Shank", "Short Rib"];

cuts.shop = "MM MEats";

for (let i = 0; i < cuts.length; i++) {
  console.log(cuts[i]);
}

cuts.forEach((cut) => {
  console.log(cut);
  if(cut === 'Brisket') {
    continue;
  }
});

for (const index in cuts) {
  console.log(cuts[index]);
}

for (const cut of cuts) {
  if(cut === 'Brisket') {
    continue;
  }
  console.log(cut);
}

for (const [i, cut] of cuts.entries()) {
  console.log(`${cut} is the ${i + 1} item`);
}

function addUpNumbers() {
  let total = 0;
  for (const num of arguments) {
    total += num;
  }
  console.log(total);
  return total;
}

addUpNumbers(10,23,52,34,12,13,123);

const name = 'Wes Bos';
for (const char of name) {
  console.log(char);
}
```
Arrays
```Javascript
// Array.from()
function sumAll() {
  const nums = Array.from(arguments);
  return nums.reduce((prev, next) => prev + next, 0);
}
const sum = sumAll(2, 34, 23, 234, 234, 234234, 234234, 2342);
console.log(sum);

// Array.of()
const ages = Array.of(32, 15, 19, 12);
console.log(ages);

// Array.some()
const adult = ages.some(age => age >= 19);
console.log(adult);

// Array.every()
const allAdult = ages.every(age => age >= 19);
console.log(allAdult);

// Array.find()
// Array.findIndex()
const cars = [
  {
    name: "Tusan",
    likes: 100
  },
  {
    name: "Santafe",
    likes: 200
  },
  {
    name: "Genesis",
    likes: 300
  }
];
const code = "Tusan";
const car = cars.find(car => car.name === code);
const carIndex = cars.findIndex(car => car.name === code);
console.log(car);
console.log(carIndex);
```
### Spread and Rest
Spread 1
```Javascript
const featured = ["Deep Dish", "Pepperoni", "Hawaiian"];
const specialty = ["Meatzza", "Spicy Mama", "Margherita"];
// Old way
const oldWayPizzas = featured.concat.apply(featured.concat(["veg"]), specialty);
// New way
const newWayPizzas = [...featured, "veg", ...specialty];
```
Spread 2
```HTML
<body>
  <h2 class="jump">SPREADS!</h2>
  <script>
    const jump = document.querySelector(".jump");
    jump.innerHTML = [...jump.textContent].map(s => `<span>${s}</span>`).join("");
    /* Styles
    body {
      min-height: 100vh; font-family: sans-serif; background: #ffc600; text-transform: uppercase;
      display: flex; justify-content: center; align-items: center; font-size: 50px;
      color:white; text-shadow: 3px 3px 0 rgba(0,0,0,0.2);
    }
    .jump span {
      position: relative; display: inline-block; transition: transform 0.1s;
      cursor:url('http://csscursor.info/source/santahand.png'), default;
    }
    .jump span:hover {
      transform:translateY(-20px) scale(2) rotate(10deg); z-index: 1;
    }
    */
  </script>
</body>
```
Spread 3
```Javascript
const items = [
  { id: 1, text: "Your id is 1" },
  { id: 2, text: "Your id is 2" },
  { id: 3, text: "Your id is 3" },
  { id: 4, text: "Your id is 4" }
];
const index = items.findIndex(i => i.id === 4);
const newItems = [...items.slice(0, index), ...items.slice(index + 1)];
```
Rest
```Javascript
function convertCurrency(rate, ...amounts) {
  return amounts.map(amount => rate * amount);
}

const amounts = convertCurrency(1.26, 1, 4, 13, 29);
console.log(amounts);
```
