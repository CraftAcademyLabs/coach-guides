- now we have one more thing to get done together and that is to display some projects.
- We will import them from a separate json file to make 

- let's create a `projects.json` in our js folder
```json
{
  "projects": [
    {
      "id": 1,
      "title": "This is my first website",
      "description": "It is made using html, css and javascript",
      "image": "https://images.unsplash.com/photo-1514070706115-47c142769603?ixid=MXwxMjA3fDB8MHxzZWFyY2h8Nzl8fGNvZGV8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
      
    },
    {
      "id": 2,
      "title": "The ATM machine",
      "description": "This is a virtual ATM machine that is developed using Ruby",
            "image": "https://images.unsplash.com/photo-1514070706115-47c142769603?ixid=MXwxMjA3fDB8MHxzZWFyY2h8Nzl8fGNvZGV8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
    },
    {
      "id": 3,
      "title": "Fizzbuzz",
      "description": "The first game that I have developed so far.",
            "image": "https://images.unsplash.com/photo-1514070706115-47c142769603?ixid=MXwxMjA3fDB8MHxzZWFyY2h8Nzl8fGNvZGV8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
    }
  ]
}
```

- change the startpage function to this:

```javascript
const startPage = async (tab) => {
  if (tab === "About Me") {
    mainContainer.innerHTML = "<h2>About Me</h2> <p>Welcome to my portfolio, on this page you will be able to read a bit more about me";
  } else if (tab === "My Projects") {
    await displayProjects();
  } else {
    mainContainer.innerHTML = "<h2>Hello World</h2>";
  }
  mainContainer.classList.add("ui", "container");
  root.appendChild(mainContainer);
};
```

- Now lets create that displayProjects function

```javascript
const displayProjects = async () => {
  let response = await (await fetch("./js/projects.json")).json();
  debugger
}
```
- refactor it when you have the project to a separate function
- and now let's create the magic of displaying this:

```javascript
const displayProjects = async () => {
  let projects = await fetchProjects();
  mainContainer.innerHTML = ''
  const projectsContainer = document.createElement('div')
  projectsContainer.classList.add('ui', 'cards')
  projects.forEach((project) => {
    let card = document.createElement("div");
    let image = document.createElement('div')
    let cardContent = document.createElement('div')
    let cardDescription = document.createElement('div')
    card.classList.add('ui', 'card')
    image.classList.add('image')
    image.innerHTML = `<img src=${project.image}/>`
    cardContent.classList.add('content')
    cardContent.innerHTML = `<a class='header'>${project.title} </a>`
    cardDescription.classList.add('description')
    cardDescription.innerText = project.description
    card.appendChild(image)
    card.appendChild(cardContent)
    card.appendChild(cardDescription)
    projectsContainer.appendChild(card)
  })
  mainContainer.appendChild(projectsContainer)
};
```

- Puh! We have an okey looking portfolio now with some navigation functionality and we make use of a card to display our projects that we get from a separate json file.
- Show that if we add another project, it will automatically add another project. 