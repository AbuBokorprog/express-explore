# Express.JS

- Fast, unopinionated, minimalist web framework for Node.js
  Express.js হলো একটি লাইটওয়েট ও মোডার্ন ওয়েব অ্যাপ্লিকেশন ফ্রেমওয়ার্ক, যা নোড.জেএস এর উপর নির্ভর করে। এটি ওয়েব অ্যাপ্লিকেশন এবং এপিআই তৈরি করার জন্য ব্যবহার করা হয়। Express.js সিম্পল, ফ্লেক্সিবল, এবং পাওয়ারফুল হওয়ায় খুব জনপ্রিয় হয়েছে।

## Installation:

```
npm install express
yarn add express
```

OR

```
yarn add express
```

## Express()

### express.json()

Express.js এর express.json() মেথডটি হলো একটি মিডলওয়্যার, যা HTTP রিকুয়েস্টের বডির জেসন ডেটা পার্স করে নেয় এবং সেটির জন্য জাভাস্ক্রিপ্ট অবজেক্ট হিসাবে ব্যবহারকারীকে ডাটা দেয়। এটি একটি বিকল্পযুক্ত মিডলওয়্যার, যা ব্যবহার করা হয় নিম্নলিখিত মধ্যকারে জেসন বডি পার্সিং করার জন্য যখন অ্যাপ্লিকেশনের মধ্যে JSON ফর্ম্যাটের রিকুয়েস্ট ডেটা পাঠানো হয়ে থাকে।

```js
app.use(express.json());

app.post("/", (req, res) => {
  console.log(req.body);
  res.send("Home page post request");
});
// content-type: application/json;
// result: {"name": "bangladesh"}
```

### express.raw()

express.raw() হলো Express.js এর একটি মিডলওয়্যার ফাংশন যা HTTP রিকুয়েস্টের বডির মূল রকম পার্স করে। এই মিডলওয়্যার ব্যবহার করা হয় যখন বিশেষ ধরণের বাইনারি ডেটা যেমন ইমেজ, ভিডিও ইত্যাদি রিকুয়েস্টের অংশ হিসাবে প্রেরণ করা হয়। এই মিডলওয়্যারের মাধ্যমে আমরা রিকুয়েস্টের বডি ডেটা যাচাই করতে পারি এবং এক্সপ্রেস অ্যাপ্লিকেশনে সেই ডেটা প্রস্তুত করতে পারি।

```js
// রিকুয়েস্টের বডি পার্স করার জন্য express.raw() মিডলওয়্যার ব্যবহার করা হয়
app.use(express.raw());

// বাইনারি ডেটা রিসিভ করার জন্য একটি রাউট ডিফাইন করা হয়
app.post("/", (req, res) => {
  console.log(req.body); // রিকুয়েস্ট বডি প্রিন্ট করা হয়
  res.send("File uploaded successfully!");
});

// result like this:
// <Buffer 7b 0d 0a 20 20 20 20 22 6e 61 6d 65 22 3a 22 62 61 6e 67 6c 61 64 65 73 68 22 0d 0a 7d>

// we can parse data in string
// console.log(req.body.toString());
```

এখানে, রিকুয়েস্টের বডি পার্স করার জন্য express.raw() মিডলওয়্যার ব্যবহার করা হয়। এটি বাইনারি ডেটা রিসিভ করার জন্য একটি POST রাউট ডিফাইন করে এবং রিকুয়েস্ট ডেটা প্রিন্ট করে যখন / পাথে ফাইল আপলোড রিকুয়েস্ট আসে।

### express.static()

express.static() একটি বিশেষ মিডলওয়্যার ফাংশন যা Express.js এর একটি বিল্ট-ইন মিডলওয়্যার হিসাবে ব্যবহার করা হয়। এটি স্ট্যাটিক ফাইলগুলি (যেমন, HTML ফাইল, CSS ফাইল, JavaScript ফাইল, ইমেজ, ভিডিও ইত্যাদি) সার্ব করার জন্য ব্যবহৃত হয়। এই মিডলওয়্যারটি ব্রাউজারে স্ট্যাটিক ফাইলগুলি প্রেরণ করার জন্য ব্যবহৃত হয়। উদাহরণস্বরূপ, আপনি স্ট্যাটিক ফাইলগুলি যেমন public ফোল্ডারে সংরক্ষণ করতে পারেন এবং এই মিডলওয়্যার ব্যবহার করে সেগুলি এক্সপ্রেস অ্যাপ্লিকেশনের রেস্পন্সে প্রেরণ করতে পারেন।

```js
// স্ট্যাটিক ফাইল সেরেভ করতে express.static() মিডলওয়্যার ব্যবহার করা হয়
app.use(
  express.static(`${__dirname}/public/`, {
    index: "home.html",
  })
);
//সব সময় ফুল পাথ লাগবে আর যদি ফাইলের নাম index না হয় তাহলে {index: 'home.html' or others এই ভাবে ডিফাইন্ড করে দিতে হবে।}
// http://localhost:5000/html/
```

### express.router()

express.router() হলো একটি রাউটার মিডলওয়্যার ফাংশন যা Express.js এর একটি বিল্ট-ইন মিডলওয়্যার হিসাবে ব্যবহার করা হয়। এটি রাউটিং টেবিল তৈরি করে যা এক্সপ্রেস অ্যাপ্লিকেশনের বিভিন্ন রাউটগুলির জন্য রিকুয়েস্ট করার সময় যে বিভিন্ন হ্যান্ডলার ফাংশন কল করতে হবে তা নির্ধারণ করে। এই মিডলওয়্যারটি আপনাকে অ্যাপ্লিকেশনের রাউটিং ব্যবস্থাপনা করতে সাহায্য করে এবং কোড গুলির সংরক্ষণ ও পরিচালনা করার সুযোগ প্রদান করে।

```
const router = express.Router([options])
```

```js
// রাউটার মিডলওয়্যার ব্যবহার করা হয়
const router = express.Router();

// রাউটার caseSensitive	না, যদি caseSensitive	করতে চান তাহলে নিম্ন লিখিত নিয়মে লেখতে হবে।

// const router = express.Router({
//   caseSensitive: true,
// });

app.use(router);

router.get("/", (req, res) => {
  res.send("Home Page");
});

router.get("/about", (req, res) => {
  res.send("About Page");
});
```

### express.text()

express.text(): এই মিডলওয়্যারটি ব্যবহার করা হয় যখন রিকুয়েস্টের বডি মূলত টেক্সট ফর্ম্যাটে থাকে।

```js
app.use(express.text());

// টেক্সট ফরমেট ডেটা রিসিভ করার জন্য একটি রাউট ডিফাইন করা হয়
app.post("/", (req, res) => {
  console.log(req.body); // রিকুয়েস্ট বডি প্রিন্ট করা হয়
  res.send("File uploaded successfully!");
});
```

/textdata রাউটে express.text() মিডলওয়্যার ব্যবহার করা হয় যেখানে টেক্সট ডেটা পার্স করা হয়।

### express.urlencoded()

express.urlencoded(): এই মিডলওয়্যারটি ব্যবহার করা হয় যখন রিকুয়েস্টের বডি ফর্ম ডেটা হিসাবে আসে, যেটি প্রায়শই এক্সপ্রেস ফর্মের মাধ্যমে ফর্মে থাকে।

```js
// ফর্ম ডেটা পার্স করার জন্য express.urlencoded() মিডলওয়্যার ব্যবহার করা হয়
app.use(express.urlencoded());

// ফর্ম ডেটা প্রিন্ট করার জন্য একটি রাউট ডিফাইন করা হয়
app.post("/formdata", (req, res) => {
  console.log(req.body); // রিকুয়েস্ট বডি প্রিন্ট করা হয়
  res.send("Form data received successfully!");
});
```

/formdata রাউটে express.urlencoded() মিডলওয়্যার ব্যবহার করা হয় যেখানে ফর্ম ডেটা পার্স করা হয়।

## Application

### app.all()

যদি আপনি চান যে কোনো একটি রাউটে যেই কোনো মেথডেই কল করা হোক না কেন পেজ বা ডাটা দেখাবে তখন app.all ব্যবহার করা হয়।

#### Example:

```js
app.all("/universel", (req, res) => {
  console.log("This is universel page");
});
```

### app.enable() & app.disable()

কোনো সিস্টেম কে ইনেবল বা ডিজেবল করার জন্য এই মেথড গুলো ব্যবহার করা হয়।

#### Example:

```js
app.enable(case sensitive routing);
app.disable(case sensitive routing);
```

### app.get(path, callback)

কোনো পেজ বা ডাটা পেতে চাইলে এই মেথড ব্যবহার করা হয়।

#### Example:

```js
app.get("/", (req, res) => {
  console.log("This is home page");
});
```

### app.set(name, data)

যদি কোনো ডাটা সেট করতে হয় তাহলে সেট(set) মেথড ব্যবহার করা হয়।

#### Example

```javascript
app.set("title", "My Sites");
```

### app.get(name)

যদি কোনো ডাটা সেট করা হয় এবং সেট করা ডাটা পেতে চাইলে গেট(get) মেথড ব্যবহার করা হয়।

#### Example

```javascript
app.set("title", "My Sites");
app.set("title");
```

### app.param()

app.param() একটি Express.js মেথড যা একটি রিকুয়েস্টের মধ্যে প্যারামিটারের মানকে পরিচালনা করে। এটি দ্বারা রিকুয়েস্টের প্যারামিটার মান প্রকাশের পূর্বে রিকুয়েস্ট অবজেক্টে নির্ধারিত মধ্যবর্তী মিডলওয়্যার ফাংশনগুলি অনুসরণ করে। এটি সাধারণত রুট প্যারামিটার প্রস্তুত এবং রিকুয়েস্ট অবজেক্টে অ্যাট্যাচ করার জন্য ব্যবহৃত হয়।

#### Example

```javascript
app.param("id", (req, res, next, name) => {
  console.log("Name parameter:", name);
  req.userDetails = name;

  next();
});

// আইডি প্যারামিটার ব্যবহার করা হয়
app.get("/users/:id", (req, res) => {
  // userDetails টা আমরা এখান থেকে পেতে পারি।
  console.log(req.userDetails);
  res.send("User: " + req.params.name);
});
```

### app.route()

app.route() মেথডটি একটি ব্যবহারিক উপায় যাতে আপনি একই পাথের বিভিন্ন HTTP মেথড রিকুয়েস্টের জন্য একই হ্যান্ডলার ফাংশন ব্যবহার করতে পারেন। এটি কোড লেখার সাথে সাথে কোড ক্লিয়ারিটি বাড়াতে সাহায্য করে এবং একই পাথের বিভিন্ন মেথডগুলির হ্যান্ডলিং সহজ করে তোলে।

```js
// app.route() মেথড ব্যবহার করে একই পাথের বিভিন্ন HTTP মেথডের হ্যান্ডলার ফাংশন ব্যবহার করা
app
  .route("/books")
  .get((req, res) => {
    res.send("Get all books");
  })
  .post((req, res) => {
    res.send("Create a new book");
  })
  .put((req, res) => {
    res.send("Update all books");
  })
  .delete((req, res) => {
    res.send("Delete all books");
  });
```

### app.engine()

app.engine() method in Express.js, which is used to set up template engines for rendering dynamic content. Template engines allow you to use static template files in your application and inject dynamic data into them.

One popular template engine used with Express.js is EJS (Embedded JavaScript).

```
npm i ejs
```

OR

```
yarn add ejs
```

```js
app.set("view engine", "ejs");

// Define a route to render an EJS template
app.get("/", (req, res) => {
  const data = {
    title: "Welcome to my Express App!",
    message: "This is a dynamic message rendered using EJS.",
  };
  res.render("index", data); // Renders the 'index.ejs' template with the provided data
});
```

### EJS

creating EJS app template

```
express --view=ejs myapp
```

## Request()

The req object represents the HTTP request
Known as req

## Response

The res object represents the HTTP response
Known as res

## Middleware

Middleware is a simple function that have accepts to req res object and next function.

### What middleware can do:

- execute any code
- can change the req and res object
- can end req/res cycle
- call nest middleware by next()
- throw & catch errors

### Type of middleware

- Application level middleware
- Router level middleware
- Error handling middleware
- built-in middleware
- third party middleware
- Configurable middleware

#### Application level middleware

These middleware functions are bound to the app object using app.use() or similar methods. They are executed for every request to the server.

```js
// Logger middleware
app.use((req, res, next) => {
  console.log(
    `${req.method} - ${req.originalUrl} - ${new Date(
      Date.now()
    ).toLocalString()}`
  );
  next();
});

// Route
app.get("/", (req, res) => {
  res.send("Hello World!");
});
```

#### Router level middleware

These middleware functions are bound to an instance of express.Router(). They are similar to application-level middleware but are bound to specific routes.

```js
const adminRouter = express.Router();

// Logger middleware for the router
adminRouter.use((req, res, next) => {
  console.log(`Router middleware: ${req.method} ${req.url}`);
  next();
});
// You can create middlewares like this:

// const logger = (req, res, next) => {
//   console.log(`Router middleware: ${req.method} ${req.url}`);
//   next();
// };

// adminRouter.use(logger)

// Route
adminRouter.get("/dashboard", (req, res) => {
  res.send("Dashboard");
});

// Mount the router at /admin/dashboard
app.use("/admin", adminRouter);
```

#### Error handling middleware

These middleware functions take four arguments instead of three (err, req, res, next) and are used to handle errors that occur during the execution of previous middleware functions.

```javascript
// middleware function 1
app.use((req, res, next) => {
  throw new Error("This is a Test error");
});

// Error handling middleware
app.use((err, req, res, next) => {
  console.error(err.message);
  res.status(500).send("Error: " + err.message);
});

// Route
app.get("/", (req, res) => {
  res.send("This is home page get method");
});
```

#### Third party middleware

Cokkie parser is a third party middleware.

```
npm i cookie-parser
```

```js
const cookieParser = require("cookie-parser");
app.use(cookieParser());
```

### Configurable middleware

## Router

### router.all()

This method handles all HTTP methods for a given route.

```js
const express = require("express");
const router = express.Router();

router.all("/users", (req, res, next) => {
  console.log("Accessing users...");
  next(); // Pass control to the next handler
});

// Handles all HTTP methods (GET, POST, PUT, DELETE) for '/users' route
router.all("/users", (req, res) => {
  res.send("All users data");
});
```

### router.METHOD()

Shorthand methods for different HTTP methods (GET, POST, PUT, DELETE, etc.).

```js
router.get("/users", (req, res) => {
  res.send("GET: List of users");
});

router.post("/users", (req, res) => {
  res.send("POST: Create new user");
});

router.put("/users/:id", (req, res) => {
  res.send(`PUT: Update user with ID ${req.params.id}`);
});

router.delete("/users/:id", (req, res) => {
  res.send(`DELETE: Delete user with ID ${req.params.id}`);
});
```

### router.route()

```js
router
  .route("/users")
  .get((req, res) => {
    res.send("GET: List of users");
  })
  .post((req, res) => {
    res.send("POST: Create new user");
  })
  .put((req, res) => {
    res.send(`PUT: Update user with ID ${req.params.id}`);
  })
  .delete((req, res) => {
    res.send(`DELETE: Delete user with ID ${req.params.id}`);
  });
```

### router.use()

Mounts middleware functions or sub-routers to a specific path in the router's route stack.

```js
// Middleware function
const logMiddleware = (req, res, next) => {
  console.log("Logging...");
  next();
};

// Mount middleware for '/users' route
router.use("/users", logMiddleware);

// Mount sub-router for '/products' route
router.use("/products", productRouter);
```

### router.param()

Defines route parameters for routes within the router.

```js
// Route parameter middleware
router.param("id", (req, res, next, id) => {
  console.log(`ID parameter: ${id}`);
  next();
});

// Route using parameter
router.get("/users/:id", (req, res) => {
  res.send(`User ID: ${req.params.id}`);
});
```

## Error Handling

### For Syncronous Code

```js
// Global Error
app.use(err, req, res, next) => {
  if(err.message){
    res.status(500).send(err.message);
  }else{
    res.send("There was an error")
  }
};
```

#### not found error:

```js
// not found error, global error doesn't catch it.
app.use(req, res, next) => {
  res.status(404).send("Request url is not found")
}
// We can also send error in Next function
next("Request url is not found");
// The error goig to global error
```

#### headerSent

```js
app.use((req, res, next) => {
  if (res.headersSent) {
    next("There was an problem");
  } else {
    if (err.message) {
      res.status(500).send(err.message);
    } else {
      res.send("There was an error!");
    }
  }
});
```

### For Asyncronous Code

## Multer

Multer is a node.js middleware for handling multipart/form-data, which is primarily used for uploading files. It is written on top of busboy for maximum efficiency.

### Installation

```
 npm install --save multer
```

```
 yarn add --save multer
```

### Basic usage example:

Don't forget the enctype="multipart/form-data" in your form.

```html
<form action="/profile" method="post" enctype="multipart/form-data">
  <input type="file" name="avatar" />
</form>
```

```js
const express = require("express");
const multer = require("multer");
const upload = multer({ dest: "uploads/" });

const app = express();

app.post("/profile", upload.single("avatar"), function (req, res, next) {
  // req.file is the `avatar` file
  // req.body will hold the text fields, if there were any
});

app.post(
  "/photos/upload",
  upload.array("photos", 12),
  function (req, res, next) {
    // req.files is array of `photos` files
    // req.body will contain the text fields, if there were any
  }
);

const cpUpload = upload.fields([
  { name: "avatar", maxCount: 1 },
  { name: "gallery", maxCount: 8 },
]);
app.post("/cool-profile", cpUpload, function (req, res, next) {
  // req.files is an object (String -> Array) where fieldname is the key, and the value is array of files
  //
  // e.g.
  //  req.files['avatar'][0] -> File
  //  req.files['gallery'] -> Array
  //
  // req.body will contain the text fields, if there were any
});
```

### .single(fieldname)

Accept a single file with the name fieldname. The single file will be stored in req.file.

<!-- Single file upload -->

```html
<form action="/profile" method="post" enctype="multipart/form-data">
  <input type="file" name="avatar" />
</form>
```

```js
const multer = require("multer");

// prepare the final multer upload object
// dest = upload file path
const upload = multer({ dest: "uploads/" });

// Only one file upload
app.post("/profile", upload.single("avatar"), function (req, res, next) {
  // req.file is the `avatar` file
  // req.body will hold the text fields, if there were any
});
```

### .array(fieldname[, maxCount])

Accept an array of files, all with the name fieldname. Optionally error out if more than maxCount files are uploaded. The array of files will be stored in req.files.

<!-- Multiple file upload -->

```html
<form action="/profile" method="post" enctype="multipart/form-data">
  <input type="file" name="avatar" multiple />
</form>
```

```js
const multer = require("multer");

// prepare the final multer upload object
// dest = upload file path
const upload = multer({ dest: "uploads/" });

// upload multiple files
// upload.array() accepts 2 parameters
// 1st is name of the uploaded input name and 2nd is the maximum how many files upload.

app.post(
  "/photos/upload",
  upload.array("photos", 3),
  function (req, res, next) {
    // req.files is array of `photos` files
    // req.body will contain the text fields, if there were any
  }
);
```

### .fields(fields)

Accept a mix of files, specified by fields. An object with arrays of files will be stored in req.files.

fields should be an array of objects with name and optionally a maxCount. Example:

```
[
  { name: 'avatar', maxCount: 1 },
  { name: 'gallery', maxCount: 8 }
]
```

<!-- Multiple file input and multiple upload -->

```html
<form action="/profile" method="post" enctype="multipart/form-data">
  <input type="file" name="avatar" multiple />
  <input type="file" name="gallery" multiple />
</form>
```

```js
//  upload.fields([
//     { name: "avatar", maxCount: 3 },
//     { name: "gallery", maxCount: 2 },
//   ]),
app.post(
  "/photos/upload",
  upload.fields([
    { name: "avatar", maxCount: 3 },
    { name: "gallery", maxCount: 2 },
  ]),
  function (req, res, next) {
    // req.files is array of `photos` files
    // req.body will contain the text fields, if there were any
  }
);
```

### .none()

Accept only text fields. If any file upload is made, error with code "LIMIT_UNEXPECTED_FILE" will be issued.

### limits

An object specifying the size limits of the following optional properties. Multer passes this object into busboy directly, and the details of the properties can be found on busboy's page.

The following integer values are available:

Key Description Default

- _fieldNameSize_ Max field name size 100 bytes
- _fieldSize_ Max field value size (in bytes) 1MB
- _fields_ Max number of non-file fields Infinity
- _fileSize_ For multipart forms, the max file size (in bytes) Infinity
- _files_ For multipart forms, the max number of file fields Infinity
- _parts_ For multipart forms, the max number of parts (fields + files) Infinity
- _headerPairs_ For multipart forms, the max number of header key=>value pairs to parse 2000
  Specifying the limits can help protect your site against denial of service (DoS) attacks.

### fileFilter

Set this to a function to control which files should be uploaded and which should be skipped. The function should look like this:

```js
function fileFilter(req, file, cb) {
  // The function should call `cb` with a boolean
  // to indicate if the file should be accepted

  // To reject this file pass `false`, like so:
  cb(null, false);

  // To accept the file pass `true`, like so:
  cb(null, true);

  // You can always pass an error if something goes wrong:
  cb(new Error("I don't have a clue!"));
}
```

_For better understanding_

```js
const upload = multer({
  dest: "uploads/",
  limits: {
    fileSize: 10000,
  },
  fileFilter: (req, file, cb) => {
    if (
      file.mimeType === "image/png" ||
      file.mimeType === "image/jpg" ||
      file.mimeType === "image/jpeg"
    ) {
      cb(null, true);
    } else {
      cb(new Error("Only jpg, png and jpeg file allowed!"), false);
    }
  },
});
```

### Multer Error Handling

```js
app.use((err, req, res, next) => {
  if (err) {
    if (err instanceof multer.MulterError) {
      res.status(500).send("There was an upload error");
    } else {
      res.status(500).send(err.message);
    }
  } else {
    res.send("success");
  }
});
```

### storage

#### DiskStorage

The disk storage engine gives you full control on storing files to disk.

```js
const storage = multer.diskStorage({
  destination: (req, file, cb) => {
    cb(null, "uploads/");
  },
  fileName: (req, file, cb) => {
    const fileExt = path.extname(file.originalname);
    const fileName =
      file.originalname
        .replace(fileExt, "")
        .tolowerCase()
        .split(" ")
        .join("-") + Date.now();
    cb(null, fileName + fileExt);
  },
});

const upload = multer({ storage: storage });
```
