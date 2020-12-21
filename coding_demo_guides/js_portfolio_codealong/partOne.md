We will code along to create a portfolio in javascript. We will create the exact same functionality that we will build in React later this week.
The reason we are doing it in Javascript is to recap and connect back to javascript as you know it, but also to give you some code that you can look back at when building your portfolio to try to connect to how React is working.
We are doing this as a code along to start to practice that early on in the bootcamp.

```
mkdir && cd portfolio_js
```

- initialize git and yarn
- create this folder structure:

```
js_portfolio_codealong/
├── css
│   └── styles.css
├── index.html
├── js
│   └── index.js
└── package.json
```

- in the index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="./css/styles.css" />
    <title>My portfolio</title>
  </head>
  <body>
    <div id="root"></div>
    <script src="./js/index.js"></script>
  </body>
</html>
```

```javascript
const root = document.getElementById("root");

const startPage = () => {
  let content = document.createElement("h1");
  content.innerText = "Hello World"
  root.appendChild(content);
};

document.addEventListener("DOMContentLoaded", () => {
  startPage();
});
```
- Okey, we have a hello world. Pretty complicated instead of just writing hello world straight in the div, but we will work extensively with javascript today

```javascript
const root = document.getElementById("root");

const header = () => {
  let nav = document.createElement('nav')
  let headerContent = document.createElement('h1')
  headerContent.innerText = 'My Portfolio'
  nav.appendChild(headerContent)
  root.appendChild(nav)
}

const startPage = () => {
  let content = document.createElement("h2");
  content.innerText = "Hello World"
  root.appendChild(content);
};

const footer = () => {
  let footer = document.createElement('footer')
  footer.innerHTML = '<h4>Made with Html, CSS and Javascript</h4>'
  root.appendChild(footer)
}

document.addEventListener("DOMContentLoaded", () => {
  header();
  startPage();
  footer()
});
```

- It looks like shit, right? Let's add a CSS framework, to get some help with the styling. 

- add these links before our own style link:

``` html
 <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/semantic-ui@2.4.2/dist/semantic.min.css">
  <script src="https://cdn.jsdelivr.net/npm/semantic-ui@2.4.2/dist/semantic.min.js"></script>

```
- You should see the the font changing. 

- Let's style our header: 
```javascript
const header = () => {
  let headerContainer = document.createElement('div')
  headerContainer.classList.add("ui", "inverted", "segment");
  let nav = document.createElement('nav')
  nav.classList.add('ui', 'inverted', 'secondary', 'menu')
  let headerContent = document.createElement('a')
  headerContent.classList.add('item')
  headerContent.innerText = 'My Portfolio'
  headerContainer.appendChild(nav);
  nav.appendChild(headerContent)
  root.appendChild(headerContainer)
}
```
Add this to your css file, to style our footer: 
```css
footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 60px;
  padding-top: 20px;
  padding-bottom: 20px;
  background-color: #f5f5f5;
  margin-bottom: 0;
  margin-top: 0;
  text-align: center;
}
```
- let's add a container to the start page content, to get some margin.

```javascript
const startPage = () => {
  let startPageContainer = document.createElement('div')
  startPageContainer.classList.add('ui', 'container')
  let content = document.createElement("h2");
  content.innerText = "Hello World"
  startPageContainer.appendChild(content)
  root.appendChild(startPageContainer);
};
```

