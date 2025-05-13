---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /assets/intro.jpg
# some information about your slides (markdown enabled)
title: Software Development | Foundations
info: |
  ## Software Development | Foundations
# apply unocss classes to the current slide
class: text-left
drawings:
  persist: false
transition: slide-left
mdc: true
---

# EJS, Agile Practices
Full-Stack Development - part 1/8
- [ ] EJS
- [ ] Refactor App
- [ ] Agile & Scrum

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
-->

---
transition: slide-left
---

# Review

- "Full-stack" combines both frontend and backend of a web application
   - can build complete apps from start to finish
   - often handles APIs, auth, databases and deployment
- List some of the various tech-stacks for web dev.  Which one will we be using?
- Read ["Manifesto for Agile Software Development"](https://agilemanifesto.org/principles.html)



---
transition: slide-left
---

# Refactor App v.3
Use what you will learn here to help build your mid-term

1. Initialize a new Node.js project set up with all folders, routes, controllers, models etc. and any other necessary components


---
transition: slide-left
---

# pg2

1. In `/src/handlers/user.js`:

---
transition: slide-left
---

# pg3
Let's create sign-in functionality

1. In `server.js`

---
transition: slide-left
---

# pg4

1. in `/src/controlllers/userController.js`

---
transition: slide-left
---

# pg5

1. in `/src/handlers/user.js`

---
transition: slide-left
---

# pg6

1. Let's put back our `protect` guard function. In `server.js`

---
transition: slide-left
---

# Exercise JWT

3. If successful, you should be able to:




---
layout: image-right
transition: slide-left
image: /assets/bos.png
backgroundSize: 500px 300px
class: text-left
---

# 10 minute break

🍦 Cool Tips, Trends and Resources:
- 🤓 [Learn Anything](https://learn-anything.xyz/)
- 🥪 [CSS :has()](https://x.com/wesbos/status/1737148340322652632)
- 🦸‍♂️ [GSAP Now Free](https://gsap.com/pricing/)
- 🛏️ [How did REST come to mean Opposite of REST](https://htmx.org/essays/how-did-rest-come-to-mean-the-opposite-of-rest/)

<br>
<hr>
<br>

- 🧪 [Enter anonymous lab questions](https://docs.google.com/forms/d/e/1FAIpQLSevvGARdHQikso-uLqFCO481MABKE5HofuSrlzEPMNQ2ZLykw/viewform?usp=dialog)
- ℹ️ [Course feedback survey](https://circuitstream.typeform.com/to/ZoyYk7px#course_id=SoftwareAN&instructor=9514)

<!-- 
- take attendance
-->

---
transition: slide-left
---

# Refactor / Tidy

- Move our get `/` route into our routes file as well
- Change `app.use("/api", router)` to `app.use("/", router);`
- Cut/paste our `app.get("/"...)` into our `router.js` file as `router.get("/"...)`
- Refactor all our `/api/order` routes to now be prepended with `/api/whatever` 
- Insert 2 new routes related:
  ```js
  router.get("/user", userController.createUser);
  router.get("/login", userController.loginUser);
  ```
- `import userController from "./controllers/userController.js"`

---
transition: slide-left
--- 

# Passport (pg.1)

- https://www.passportjs.org/packages/
- `npm i passport passport-local-mongoose express-session connect-mongo`
  ```js
  import passport from 'passport'; // in server.js
  import session from 'express-session';
  import MongoStore from 'connect-mongo';
  import User from "./models/user.js";

  // passport-local-mongoose provides .createStrategy() which uses passport-local under the hood
  passport.use(User.createStrategy()); 
  passport.serializeUser(User.serializeUser()); // upon successful login writes user ID to session
  passport.deserializeUser(User.deserializeUser()); // called on every request that has a session which then reads user ID from session, and populates req.user
  
  app.use(session({  
    secret: process.env.PASSPORT_SECRET, // remember to input this in .env
    key: process.env.PASSPORT_COOKIE_KEY,  // remember to input this in .env
    resave: false,
    saveUninitialized: false,
    store: MongoStore.create({ mongoUrl: process.env.DB_CONN}) // store sessions in mongoDB (not in memory)
  }));

  app.use(passport.initialize()); 
  app.use(passport.session());
  ```

---
transition: slide-left
---

# Passport (pg.2)

- Create new route to:
  ```js
  router.get("/register", userController.registerForm);
  router.get("/login", userController.loginForm);
  ```
- Create new controller functions in `/src/controllers/userController.js`
  ```js
  const registerForm = async (req, res) => {
    res.render("register", { title: "Register" });
  };

  const loginForm = async (req, res) => {
    res.render("login", { title: "Login" });
  };
  ```
- Create new login.ejs and register.ejs pages

---
transition: slide-left
---

# Passport (pg.3)

- in `/src/models/user.js`:
  ```js
  import mongoose from "mongoose";
  import plm from "passport-local-mongoose"; 

  const userSchema = mongoose.Schema({
    username: {
      type: String,
      required: true,
      unique: true,
    },
    password: {
      type: String,
      required: true, // hashed password
    },
  });

  // below adds username, hash and salt fields,
  // and will store username, hashed password and salt value
  userSchema.plugin(plm); 

  export default mongoose.model("user", userSchema);
  ```
- Test it


---
transition: slide-left
---

# Exercise Passport

1. Try incorporating the signup, the login using .ejs pages


---
transition: slide-left
---

# Homework

- Make a To-Do List App with MongoDB [see instructions in LMS](https://courses.circuitstream.com/d2l/le/lessons/9514/topics/49825)