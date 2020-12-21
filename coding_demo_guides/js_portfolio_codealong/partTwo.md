- Okey let's continue on our portfolio and now we will add some navigation. 

- First let's add some more buttons to our header

```javascript
const header = () => {
  let headerContainer = document.createElement('div')
  headerContainer.classList.add("ui", "inverted", "segment");
  let nav = document.createElement('nav')
  nav.classList.add('ui', 'inverted', 'secondary', 'menu')
  let tabs = ['My Portfolio', 'About Me', 'My Projects']
  tabs.forEach(tab => {
    const tabLink = document.createElement('a')
    tabLink.classList.add('item')
    tabLink.innerText = tab
    nav.appendChild(tabLink)
  })
  headerContainer.appendChild(nav);
  root.appendChild(headerContainer)
}
```
- okey and now we need to make them clickable and we want the content on the page to change depending on which button we click
- Let's add this to header and the tabs iterator
```javascript
  tabLink.addEventListener('click', () => startPage(tab))
```
- And update the startPage like this:
```javascript
const startPage = (tab) => {
const startPage = async (tab) => {
  if (tab === "About Me") {
    mainContainer.innerHTML = "<h2>About Me</h2> <p>Welcome to my portfolio, on this page you will be able to read a bit more about me";
  } else if (tab === "My Projects") {
    mainContainer.innerHTML = "<h2>My Projects</h2> <p>Welcome to my portfolio, on this page you will be able to read a bit more the projects that I have done";
  } else {
    mainContainer.innerHTML = "<h2>Hello World</h2>";
  }
  mainContainer.classList.add("ui", "container");
  root.appendChild(mainContainer);
};
  mainContainer.classList.add("ui", "container");
  root.appendChild(mainContainer);
};
```
- Also this has to go to the top of the file:
```javascript
const mainContainer = document.createElement("div");
```


If there is time to add active item
```javascript
const removeActive = (tab) => {
  let areActive = document.querySelectorAll(".active");
  if (areActive.length > 0) {
    areActive[0].classList.remove("active");
  }
  tab.classList.add("active");
};
```

