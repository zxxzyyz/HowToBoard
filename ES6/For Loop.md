### For Loop
Loop
```Javascript
const cuts = ["Chuck", "Brisket", "Shank", "Short Rib"];
cuts.shop = "MM MEats";

// cuts.shop is undefined
for (let i = 0; i < cuts.length; i++) {
  console.log(cuts[i]);
}

// continue is not allowed
cuts.forEach((cut) => {
  console.log(cut);
  if(cut === 'Brisket') {
    continue;
  }
});

// cuts.shop is undefined
for (const index in cuts) {
  console.log(cuts[index]);
}

// continue is allowed and skips cut.shop
for (const cut of cuts) {
  if(cut === 'Brisket') {
    continue;
  }
  console.log(cut);
}

// cuts.shop is undefiend
for (const [i, cut] of cuts.entries()) {
  console.log(`${cut} is the ${i + 1} item`);
}

// Looping string
const name = 'Wes Bos';
for (const char of name) {
  console.log(char);
}
```
```Javascript
Use of Arguments
function addUpNumbers() {
  let total = 0;
  for (const num of arguments) {
    total += num;
  }
  console.log(total);
  return total;
}
addUpNumbers(10,23,52,34,12,13,123);
```