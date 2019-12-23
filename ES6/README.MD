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
