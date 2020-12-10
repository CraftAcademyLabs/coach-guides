```
$ yarn create react-app hello_world
```
During this week you will not use this CLI but actually create all that is scaffolded for me right now by yourselves, to see how much configuration it is in there!

Happy hacking! lets have a look at what we scaffholded

```
$ cd hello_world
```
As you can see, we already have git initialized when we create a react-app, so we do not need to do gitinit or anything 
```
$ code . 
```
```
$ yarn start
```
Just to show how the scaffold looks like
Go back to VS and show how the folderstructure is. 
Clean up files so it ends up like this:
```
├── README.md
├── node_modules
├── package.json
├── public
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
├── src
│   ├── App.jsx
|   ├── index.css
│   ├── index.js
│   └── serviceWorker.js
└── yarn.lock
```
Go into the files and explain a bit, clean up comments

rce in VS to open class component, remove the export

```
  state = {
    greeting: 'Hello'
  }
  render() {
    return (
      <div>
        {this.state.greeting} World
      </div>
    )
  }

```
```
state = {
    greeting: 'Hello'
  }
  onClickHandler = () => {
    this.setState({
      greeting: 'Good Morning'
    })
  }
  render() {
    return (
      <div>
        {this.state.greeting} World
        <button onClick={this.onClickHandler}>Click Me</button>
      </div>
    )
  }
```
```
state = {
    greeting: 'Hello',
    message: 'World'
  }
  greetingHandler = () => {
    this.setState({
      greeting: 'Good Morning'
    })
  }
  messageHandler = () => {
    this.setState({
      message: 'Juniors'
    })
  }

  render() {
    return (
      <div>
        {this.state.greeting} {this.state.message}
        <button onClick={this.greetingHandler}>Greeting</button>
        <button onClick={this.messageHandler}>Message</button>
      </div>
    )
  }
```
 