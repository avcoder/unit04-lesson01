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

# pg3
Let's create sign-in functionality

asdf

---
transition: slide-left
---

# pg4

asdf

---
transition: slide-left
---

# pg5

asdf

---
transition: slide-left
---

# pg6

asdf

---
transition: slide-left
---

# Exercise JWT

asdf




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

# pg4

- in `/src/models/user.js`:


---
transition: slide-left
---

# Homework

- Start working on your midterm note-taking app