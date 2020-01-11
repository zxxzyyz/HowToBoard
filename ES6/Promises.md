### Promises
Usage 1
```Javascript
const users = fetch('https://jsonplaceholder.typicode.com/users');
users
  .then(potato => potato.json())
  .then(apple => { console.log(apple) })
  .catch((err) => { console.log(err) });
```
Usage 2
```Javascript
// Assume that posts and authors are tables in database
// Assume that properties are columns of tables
const posts = [
  { title: "I love JavaScript", author: "Wes Bos", id: 1 },
  { title: "CSS!", author: "Chris Coyier", id: 2 },
  { title: "Dev tools tricks", author: "Addy Osmani", id: 3 }
];
const authors = [
  { name: "Wes Bos", twitter: "@wesbos", bio: "Canadian Developer" },
  { name: "Chris Coyier", twitter: "@chriscoyier", bio: "CSS Tricks and CodePen" },
  { name: "Addy Osman", twitter: "@addyosmani", bio: "Googler" }
];

function getPostById(id) {
  return new Promise((resolve, reject) => {
    // Assume that it takes 1 second to retrieve data from database
    setTimeout(() => {
      const post = posts.find(post => post.id === id);
      if (post) {
        resolve(post);
      } else {
        reject(Error("No post found"));
      }
    }, 1000);
  });
}

function hydrateAuthor(post) {
  return new Promise((resolve, reject) => {
    // Assume that it takes 1 second to retrieve data from database
    setTimeout(() => {
      const author = authors.find(author => author.name === post.author);
      if (author) {
        post.author = author;
        resolve(post);
      } else {
        reject(Error("No author was found"));
      }
    }, 1000);
  });
}

getPostById(3)
  .then(post => {
    console.log("resolved post");
    return hydrateAuthor(post);
  })
  .then(post => {
    console.log("resolved new post");
    console.log(post);
  })
  .catch(err => {
    console.error(err);
  });
```
Usage 3
```Javascript
// There are 200 todos
const listOfTodos = fetch('https://jsonplaceholder.typicode.com/todos');
// There are 5000 photos
const listOfPhotos = fetch('https://jsonplaceholder.typicode.com/photos');

// Multiple Promises
Promise
  .all([listOfTodos, listOfPhotos])
  .then(responses => {
    return Promise.all(responses.map(response => response.json()))
  })
  .then(responses => {
    console.log(responses);
  }).catch(err => {
    console.error(err);
  });
```