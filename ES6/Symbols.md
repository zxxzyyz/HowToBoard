### Symbols
```Javascript
const koo = Symbol("JavaScript");
const jungmin = Symbol("JavaScript");
console.log(koo);
console.log(jungmin);

const classRoom = {
  [Symbol('Mark')] : { grade: 50, gender: 'male' },
  [Symbol('olivia')]: { grade: 80, gender: 'female' },
  [Symbol('olivia')]: { grade: 80, gender: 'female' },
};

for (const student in classRoom) {
  console.log(student);
}

const syms = Object.getOwnPropertySymbols(classRoom);
const data = syms.map(sym => classRoom[sym]);
console.log(data);
```
