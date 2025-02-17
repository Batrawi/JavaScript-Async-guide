# JavaScript Callbacks, Promises, and Async/Await

## 📌 Callbacks

A **callback function** is a function that is **passed as an argument** to another function and executed **later** after some operation is completed.

### 💡 Why do we use Callbacks?
- JavaScript is **asynchronous**, meaning it doesn't wait for tasks to complete before moving on.
- Callbacks allow code to **execute after a task is completed**, such as reading a file or making an API request.

### 🔹 How Callbacks Work

#### **Example 1: Simple Callback**
```js
function greet(name, callback) {
    console.log("Hello, " + name);
    callback(); // Call the callback function
}

function sayGoodbye() {
    console.log("Goodbye!");
}

greet("Mohammed", sayGoodbye);
```
✅ **Output:**
```
Hello, Mohammed
Goodbye!
```

### 🔹 Callbacks with Asynchronous Operations

#### **Example 2: Using `setTimeout` to Simulate Delayed Task**
```js
function fetchData(callback) {
    setTimeout(() => {
        console.log("Data fetched from database");
        callback();
    }, 2000);
}

function processData() {
    console.log("Processing data...");
}

fetchData(processData);
```
✅ **Output (after 2 seconds):**
```
Data fetched from database
Processing data...
```

### 🔹 Callbacks with Arguments

#### **Example 3: Passing Data to a Callback**
```js
function getUser(id, callback) {
    setTimeout(() => {
        console.log("Fetched user data");
        callback({ id: id, name: "Mohammed" });
    }, 1000);
}

function displayUser(user) {
    console.log("User ID:", user.id);
    console.log("User Name:", user.name);
}

getUser(101, displayUser);
```
✅ **Output (after 1 second):**
```
Fetched user data
User ID: 101
User Name: Mohammed
```

### ❌ **Problem: Callback Hell**

When multiple asynchronous operations are **nested**, it becomes **hard to read and debug**.

#### **Example 4: Callback Hell (Bad Practice)**
```js
getUser(101, (user) => {
    getPosts(user.id, (posts) => {
        getComments(posts[0].id, (comments) => {
            console.log("First comment:", comments[0]);
        });
    });
});
```
❌ **Problems:**
- Hard to **read and maintain**.
- Difficult to **debug**.
- Hard to **scale** for complex logic.

✅ **Solution:** **Use Promises and Async/Await**.

---

## 📌 Promises

A **Promise** is an object that represents a **future value** that may be available **now, later, or never**.

### 🔹 Three States of a Promise:
1. **Pending** → Initial state.
2. **Fulfilled (Resolved)** → Operation completed successfully.
3. **Rejected** → Operation failed.

### 🔹 Creating a Promise

#### **Example 5: Basic Promise**
```js
const myPromise = new Promise((resolve, reject) => {
    let success = true;
    setTimeout(() => {
        if (success) {
            resolve("Task completed successfully!");
        } else {
            reject("Task failed!");
        }
    }, 2000);
});

myPromise.then((result) => console.log(result)).catch((error) => console.log(error));
```
✅ **Output (after 2 seconds):**
```
Task completed successfully!
```

### 🔹 What `resolve()` and `.then()` Return

#### **Example 6: Understanding `resolve()`**
```js
const promise = new Promise((resolve) => {
    resolve({ id: 1, name: "Mohammed" });
});

promise.then((result) => console.log(result));
```
✅ **Output:**
```
{ id: 1, name: 'Mohammed' }
```

### 🔹 Chaining `.then()`

#### **Example 7: Chaining Promises**
```js
fetchData()
    .then((user) => {
        console.log("User fetched:", user);
        return user.name;
    })
    .then((name) => console.log("Processing:", name));
```

### 🔹 Running Multiple Promises (`Promise.all()`)

#### **Example 8: Fetching Multiple Async Data**
```js
const promise1 = new Promise((resolve) => setTimeout(() => resolve("Data 1"), 2000));
const promise2 = new Promise((resolve) => setTimeout(() => resolve("Data 2"), 1000));

Promise.all([promise1, promise2]).then((results) => console.log("All data:", results));
```
✅ **Output (after 2 seconds):**
```
All data: [ 'Data 1', 'Data 2' ]
```

---

## 📌 Async/Await

### 💡 Why Use `async/await`?
- Avoids **callback hell** and complex `.then()` chains.
- Makes **code cleaner** and **easier to debug**.
- Helps write **asynchronous functions** in a **synchronous style**.

### 🔹 Basic `async` Function

#### **Example 9: Basic `async` Function**
```js
async function greet() {
    return "Hello, Mohammed!";
}

greet().then(console.log);
```
✅ **Output:**
```
Hello, Mohammed!
```

### 🔹 Using `await` with a Promise

#### **Example 10: Waiting for a Promise**
```js
function fetchData() {
    return new Promise((resolve) => setTimeout(() => resolve("Data received!"), 2000));
}

async function getData() {
    let data = await fetchData();
    console.log(data);
}

getData();
```
✅ **Output (after 2 seconds):**
```
Data received!
```

### 🔹 Handling Errors with `try...catch`

#### **Example 11: Handling Errors in Async Functions**
```js
async function getData() {
    try {
        let data = await fetchData();
        console.log("Data:", data);
    } catch (error) {
        console.log("Error:", error);
    }
}
```

### 🔹 Running Multiple Async Tasks in Parallel (`Promise.all()`)

#### **Example 12: Fetching User and Posts in Parallel**
```js
async function getUserData() {
    let [user, posts] = await Promise.all([fetchUser(), fetchPosts(1)]);
    console.log("User:", user);
    console.log("Posts:", posts);
}

getUserData();
```
✅ **Output (after 1.5 seconds):**
```
User: { id: 1, name: 'Mohammed' }
Posts: [ 'Post 1', 'Post 2' ]
```

---

## 🔥 Final Summary

| Feature | Callbacks | Promises | Async/Await |
|---------|----------|----------|-------------|
| Readability | ❌ Hard to read | 🟢 Better than callbacks | ✅ Clean & simple |
| Error Handling | ❌ Complex | 🟢 `.catch()` | ✅ `try...catch` |
| Parallel Execution | ❌ No | 🟢 `Promise.all()` | ✅ `Promise.all()` |
| Best For | Small async tasks | Chained async operations | Clean async code |

🚀 Now you have a **deep understanding** of **callbacks, promises, and async/await**! 🎉

