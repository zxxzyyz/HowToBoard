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