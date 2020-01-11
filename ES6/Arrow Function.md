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