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

# EJS
Full-Stack Development - part 1/8
- [ ] EJS
- [ ] Refactor App

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

Initialize a new Node.js project set up with all folders, routes, controllers, models etc. and any other necessary components

- `npm init -y`
- `npm i connect-mongo cookie-parser dotenv ejs express express-session express-validator mongoose morgan passport passport-local-mongoose github-slugger connect-flash`
- `npm i -D nodemon`
- edit `package.json`
   - insert under scripts, `"start": "nodemon index.js"`
   - we'll use ES import way, so add `"type": "module",`



---
transition: slide-left
---

# Build infrastructure

- create folder structure:
   - /controllers
   - /handlers
   - /models
   - /public
   - /routes
   - /utils
   - /views
- create `.gitignore` (exclude `node_modules`, `.env`, `.DS_Store`)
- create files .env, connect.js, passport.js, index.js, app.js, /routes/router.js, /models/userModel.js

---
transition: slide-left
---

# Create EJS page and utils

- in /routes/router.js:
  ```js
  router.get("/", (req, res) => {
    res.render("home", { title: "🚚 Welcome to Food Truck!" });
  });
  ```
- in /views/home.ejs:
  ```html
  <h1><%= title %></h1>
  <p><%= currentPath %></p>
  <p><%= u.siteName %></p>
  <p><%- u.icon("zap") %></p>
  <p><%- u.dump(u.menu) %></p>
  <p><%- u.datefns.format(new Date(), "'Today is a ' eeee") %></p>
  ```
- create /utils/utils.js
- add it in app.js via middleware
- Download [Feather Icons](https://feathericons.com/)

---
transition: slide-left
---

# Add Error Handlers

- add /handlers/errorHandlers.js
  ```js
  export const catchErrors = (fn) => {
    return function (req, res, next) {
      return fn(req, res, next).catch(next);
    };
  };

  export const notFound = (req, res, next) => {
    const err = new Error("Not Found");
    err.status = 404;
    next(err);
  };
  ```

- in app.js:
  ```js
  import { notFound } from "./handlers/errorHandlers.js";

  app.use(notFound); // place near bottom after our routes
  ```

---
transition: slide-left
---

# Add Foodtruck Model
```js
import mongoose from "mongoose";
import GithubSlugger from "github-slugger";
const slugger = new GithubSlugger();
const truckSchema = mongoose.Schema({
  name: {
    type: String,
    trim: true,
    required: [true, "truck name is required"],
  },
  slug: String,
  description: {
    type: String,
    trim: true,
    maxlength: [100, "description is too long"],
  },
  tags: [String],
});
truckSchema.pre("save", function (next) {
  if (!this.isModified("name")) {
    next();
    return;
  }
  this.slug = slugger.slug(this.name);   // TODO: ensure slugs are unique
  next();
});
export default mongoose.model("Truck", truckSchema); // import it in index.js
```

---
transition: slide-left
---

# GET/POST route for adding a truck

- in /controllers/truckController.js:
  ```js
  const addTruck = (req, res) => {
    res.render("addTruck", { title: "Add Store" });
  };

  const createTruck = (req, res) => {
    const truckData = req.body;
    res.redirect("/"); // temporary for now
  };
  ```
- in /routes/router.js:
  ```js
  router.get("/add", truckController.addTruck);
  router.post("/add", truckController.createTruck);
  ```
- download foodtruck svg from [Undraw](https://undraw.co/) into /public/images/



---
transition: slide-left
---

# Create EJS for add

```html
    <h2><%= title %></h2>
    <form action="/add" method="POST">
      <label for="name">Truck Name</label>
      <input type="text" name="name" />
      <br />
      <label for="description">Description</label>
      <textarea name="description"></textarea>
      <% const choices = ['Cash only', 'Debit only', 'Online ordering',
      'Corporate lunches', 'Vegetarian'] %>
      <ul>
        <% choices.map((choice) => { %>
        <li>
          <input
            type="checkbox"
            name="tags"
            id="<%= choice %>"
            value="<%= choice %>"
          />
          <label for="<%= choice %>"><%= choice %></label>
        </li>
        <% }) %>
      </ul>
      <button type="submit">Save</button>
    </form>
```

---
transition: slide-left
---

# create Truck handler

- in `/handlers/truckHandler.js`:
  ```js
  import Truck from "../models/truckModel.js";

  const createTruck = async (truckData) => {
    return await Truck.create(truckData);
  };

  export default {
    createTruck,
  };
  ```
- in `/controllers/truckController.js`:
  ```js
  const createTruck = async (req, res) => {
    const truckData = req.body;
    await truckHandler.createTruck(truckData);
    res.redirect("/"); // temp for now
  };
  ```
- in /routes/router.js: 
  ```js
  import { catchErrors } from "../handlers/errorHandlers.js";

  router.post("/add", catchErrors(truckController.createTruck));
  ```


---
layout: image-right
transition: slide-left
image: /assets/100days.png
backgroundSize: 400px 120px
class: text-left
---

# 10 minute break

🍦 Cool Tips, Trends and Resources:
- 💯 [100 Days of Code](https://www.100daysofcode.com/)
- 🤓 [Learn Anything](https://learn-anything.xyz/)
- 🥪 [CSS has](https://x.com/wesbos/status/1737148340322652632)
- 🦸‍♂️ [GSAP Now Free](https://gsap.com/pricing/)
- 🌶️ [How did REST come to mean Opposite of REST](https://htmx.org/essays/how-did-rest-come-to-mean-the-opposite-of-rest/)

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

# GET all Foodtrucks

- in /controllers/truckController.js:
  ```js
  const getTrucks = async (req, res) => {
    const trucks = await truckHandler.getAllTrucks();
    res.render("trucks", { title: "All Trucks", trucks });
  };
  ```
- in /handlers/truckHandler.js:
  ```js
  const getAllTrucks = async () => {
    return await Truck.find().lean();
  };

  export default {
   getAllTrucks,
   createTruck
  }
  ```
- in /routes/router.js:
  ```js
  router.get("/", truckController.getTrucks);
  router.get("/trucks", truckController.getTrucks);
  ```
- create /views/trucks.ejs and /views/components/truck.ejs

---
transition: slide-left
---

# Homework

- Start working on your midterm note-taking app