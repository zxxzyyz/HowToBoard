### Object literal-upgrqades
```Javascript
const first = "koo";
const last = "jungmin";
const person = {
  first,
  last,
  test: ["1", "2"]
};
```
```Javascript
const obj1 = {
  eat: function () {},
  sleep: function () {}
};
const ojb2 = {
  eat() {},
  sleep() {}
};
```
```Javascript
function invertColor(color) {
  return '#' + ("000000" + (0xFFFFFF ^ parseInt(color.substring(1), 16)).toString(16)).slice(-6);
}

const key = "Color";
const value = "#ffc600";
const test1 = {
  [key]: value,
  [`${key}Opposite`]: invertColor(value)
};
```
```Javascript
const keys = ["size", "color", "weight"];
const values = ["medium", "red", 100];
const test = {
  [keys.shift()]: values.shift(),
  [keys.shift()]: values.shift(),
  [keys.shift()]: values.shift()
}
```