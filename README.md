# Core-Node
# Node.js HTTP Server with Form Submission

## 📌 Project Overview

This project is a simple **Node.js HTTP Server** built using only Node.js built-in modules (without Express.js).

The server performs the following tasks:

* Creates an HTTP server.
* Displays a "Hello World" message on the home page.
* Displays an HTML form.
* Receives form data using a **POST** request.
* Reads data from a text file.
* Appends the new form data to the file.
* Returns a success message after saving the data.

---

# 📁 Project Structure

```text
project/
│── index.js
│── data.txt
│── README.md
```

---

# 📦 Built-in Modules Used

## 1. http

Used to create the HTTP server.

```javascript
const http = require("http");
```

Purpose:

* Create server
* Receive requests
* Send responses

---

## 2. fs (File System)

```javascript
const fs = require("fs");
```

Used for:

* Reading files
* Writing files
* Creating files
* Updating files

---

## 3. path

```javascript
const path = require("path");
```

Used to create a safe file path that works on Windows, macOS, and Linux.

---

# 📂 File Path

```javascript
const filePath = path.join(process.cwd(), "data.txt");
```

### process.cwd()

Returns the current working directory.

Example:

```text
C:\Users\Hafiz\Desktop\project
```

### path.join()

Joins folder path with the file name.

Example:

```text
C:\Users\Hafiz\Desktop\project\data.txt
```

---

# 🚀 Creating the Server

```javascript
const server = http.createServer((req, res) => {});
```

### req (Request)

Contains information sent by the browser.

Examples:

* URL
* Method (GET/POST)
* Headers
* Body

### res (Response)

Used to send data back to the browser.

Examples:

* HTML
* Text
* JSON

---

# 🏠 Route: /

```javascript
if (req.url === "/")
```

When the browser visits:

```text
http://localhost:3000/
```

Response:

```text
hello world!
```

---

# 📝 Route: /form

```javascript
else if (req.url === "/form")
```

Displays an HTML form.

```html
<form action="/submit" method="post">
    <input name="data">
    <input name="data2">
    <button>Send</button>
</form>
```

### Form Action

```html
action="/submit"
```

After clicking the button, the form sends data to:

```text
/submit
```

### Method

```html
method="post"
```

Sends the form data inside the request body.

---

# 📨 Route: /submit

```javascript
else if (req.url === "/submit")
```

Receives the submitted form data.

---

## Receiving Data

```javascript
let data = "";
```

Creates an empty variable to store incoming data.

---

## data Event

```javascript
req.on("data", chunk => {
    data += chunk;
});
```

HTTP request data arrives in chunks.

Example:

Chunk 1

```text
data=Ali
```

Chunk 2

```text
&data2=Ahmed
```

Final Data

```text
data=Ali&data2=Ahmed
```

---

## end Event

```javascript
req.on("end", () => {});
```

Runs after all chunks have been received.

---

# 📖 Reading the File

```javascript
fs.readFile(filePath, (_, fileData) => {});
```

Reads the existing contents of **data.txt**.

Example:

```text
Ali
Ahmed
```

---

# ➕ Appending New Data

```javascript
let newData = fileData + "\n" + data;
```

If the file contains:

```text
Ali
```

And the submitted form data is:

```text
data=Ahmed&data2=Khan
```

The new file becomes:

```text
Ali
data=Ahmed&data2=Khan
```

---

# 💾 Writing Data

```javascript
fs.writeFile(filePath, newData, () => {});
```

Overwrites the file with the updated content.

---

# ✅ Success Response

```javascript
res.write("data recived!");
res.end();
```

The browser displays:

```text
data recived!
```

---

# ❌ 404 Route

```javascript
else
```

If the requested URL does not exist:

Example:

```text
http://localhost:3000/abc
```

Response:

```text
404-notfound
```

---

# 🌐 Starting the Server

```javascript
server.listen(3000);
```

Runs the server on port **3000**.

Open in your browser:

```text
http://localhost:3000
```

---

# 🔄 Request Flow

```text
Browser
   │
   ▼
HTTP Request
   │
   ▼
Node.js Server
   │
   ├── "/" → Hello World
   │
   ├── "/form" → HTML Form
   │
   ├── "/submit"
   │       │
   │       ▼
   │  Receive Form Data
   │       │
   │       ▼
   │  Read data.txt
   │       │
   │       ▼
   │  Append New Data
   │       │
   │       ▼
   │  Save File
   │       │
   │       ▼
   │  Send Success Message
   │
   ▼
404 Not Found
```

---

# 📚 Concepts Covered

* Node.js
* HTTP Module
* File System (fs)
* Path Module
* HTTP Server
* Routing
* Request (req)
* Response (res)
* GET Request
* POST Request
* HTML Forms
* Request Body
* Event-Driven Programming
* `data` Event
* `end` Event
* Callback Functions
* File Reading
* File Writing
* Basic Backend Development

---

# ▶️ How to Run

### 1. Install Node.js

Download and install Node.js from the official website.

### 2. Navigate to the Project Folder

```bash
cd project
```

### 3. Run the Server

```bash
node index.js
```

### 4. Open the Browser

Home Page

```text
http://localhost:3000/
```

Form Page

```text
http://localhost:3000/form
```

---

# 📌 Future Improvements

* Check `req.method === "POST"` before handling form submission.
* Use `fs.appendFile()` instead of reading and rewriting the whole file.
* Parse form data using the `querystring` or `URLSearchParams` API.
* Add proper error handling for `fs.readFile()` and `fs.writeFile()`.
* Return HTML pages instead of plain text.
* Migrate the project to **Express.js** for cleaner routing and middleware support.

---

# 👨‍💻 Author

**Muhammad Hafiz**

Learning Node.js Backend Development 🚀
