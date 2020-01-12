# A. New Year Garland
### time limit per test: 1 second
### memory limit per test: 256 megabytes
### input: standard input
### output: standard output

Polycarp is sad — New Year is coming in few days but there is still no snow in his city.
To bring himself New Year mood, he decided to decorate his house with some garlands.
The local store introduced a new service this year, called "Build your own garland".
So you can buy some red, green and blue lamps, provide them and the store workers will solder a single garland of them.
The resulting garland will have all the lamps you provided put in a line.
Moreover, no pair of lamps of the same color will be adjacent to each other in this garland!

For example, if you provide 3 red, 3 green and 3 blue lamps,
the resulting garland can look like this: "RGBRBGBGR" ("RGB" being the red, green and blue color, respectively).
Note that it's ok to have lamps of the same color on the ends of the garland.

However, if you provide,
say, 1 red, 10 green and 2 blue lamps then the store workers won't be able to build any garland of them.
Any garland consisting of these lamps will have at least one pair of lamps of the same color adjacent to each other.
Note that the store workers should use all the lamps you provided.

So Polycarp has bought some sets of lamps and now he wants to know if the store workers can build a garland from each of them.

Input
The first line contains a single integer t (1≤t≤100) — the number of sets of lamps Polycarp has bought.
Each of the next t lines contains three integers r, g and b (1≤r,g,b≤109)
— the number of red, green and blue lamps in the set, respectively.

Output
Print t lines — for each set of lamps print "Yes" if the store workers can build a garland from them and "No" otherwise.

Example
##### Input
```
3
3 3 3
1 10 2
2 1 1
```
##### Output
```
Yes
No
Yes
```

##### Solution
```Javascript
let testCases = Math.round(Math.random() * 100) + 1;
while (testCases) {
    solve();
    //solveBruteForce();
    --testCases;
}

function solve() {
    let a = Math.round(Math.random() * 1000000000) + 1;
    let b = Math.round(Math.random() * 1000000000) + 1;
    let c = Math.round(Math.random() * 1000000000) + 1;
    let max = Math.max(a, b, c);
    console.log(a, b, c, (max > a + b + c - max + 1) ? "Yes" : "No");
}

function solveBruteForce() {
    let last, next, result = "No";
    let a = Math.round(Math.random() * 1000000000) + 1;
    let b = Math.round(Math.random() * 1000000000) + 1;
    let c = Math.round(Math.random() * 1000000000) + 1;
    const intput = [a, b, c];
    if (a > b) {
        if (a > c) {
            last = "red";
        } else {
            last = "blue";
        }
    } else {
        if (b > c) {
            last = "green";
        } else {
            last = "blue";
        }
    }
    while (a + b + c) {
        switch (last) {
            case "red":
                if (b > c) {
                    next = "green";
                    b--;
                } else {
                    next = "blue";
                    c--;
                }
                break;
            case "green":
                if (a > c) {
                    next = "red";
                    a--;
                } else {
                    next = "blue";
                    c--;
                }
                break;
            case "blue":
                if (a > b) {
                    next = "red";
                    a--;
                } else {
                    next = "green";
                    b--;
                }
                break;
        }
        if (last === next || 0 > a || 0 > b || 0 > c) break;
        last = next;
    }
    if (a + b + c === 0) result = "Yes";
    console.log(input, result);
}
```
