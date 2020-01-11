### Arrays
Array.from()
```Javascript
function sumAll() {
  const nums = Array.from(arguments);
  return nums.reduce((prev, next) => prev + next, 0);
}
const sum = sumAll(2, 34, 23, 234, 234, 234234, 234234, 2342);
console.log(sum);
```
Array.of()
```Javascript
const ages = Array.of(32, 15, 19, 12);
console.log(ages);
```
Array.some()
```Javascript
const adult = ages.some(age => age >= 19);
console.log(adult);
```
Array.every()
```Javascript
const allAdult = ages.every(age => age >= 19);
console.log(allAdult);
```
Array.find()
Array.findIndex()
```Javascript
const cars = [
  { name: "Tusan", likes: 100 },
  { name: "Santafe", likes: 200 },
  { name: "Genesis", likes: 300 }
];
const code = "Tusan";
const car = cars.find(car => car.name === code);
const carIndex = cars.findIndex(car => car.name === code);
console.log(car);
console.log(carIndex);
```