### Class
```Javascript
class Animal {
    constructor(name) {
        this.name = name;
        this.belly = [];
    }

    eat(food) {
        this.belly.push(food);
        return this.belly;
    }


    get description() {
        return `I am ${this.name}`;
    }
}

class Dog extends Animal {
    constructor(name, breed) {
        super(name);
        this.breed = breed;
    }

    get description() {
        return `My name is ${this.name} I am ${this.breed}`;
    }

    set setage(age) {
        this.age = age;
    }

    get getage() {
        return this.age;
    }
}

const rhyno = new Animal("rhyno");
const babi = new Dog("babi", "martiz");

class MovieColletion extends Array {
    constructor(name, ...items) {
        super(...items);
        this.name = name;
    }

    topRated(limit) {
        return this.sort((a, b) => (a.star > b.star ? -1 : 1)).slice(0, limit);
    }
}

const myMovies = new MovieColletion("fav movies",
    { name: "Movie 1", star: 1 },
    { name: "Movie 2", star: 2 },
    { name: "Movie 3", star: 3 });
```
