# Getting Started
Our first objective will be to create a new React application using the create-react-app script. I'm using yarn so the command is slightly different than the one you might be used to if you are a npm user.

```
$ yarn create react-app hello_world
```
Make sure to cd into your newly created application folder and open your application in your code editor. I'm using VSCode with CLI commands enabled, and I can open my project with a single terminal command:

```
$ cd hello_world
$ code .
```

I would also suggest that you fire up the development server and take a look at your app in the browser. You can actually keep it running while you make changes to your code for the most part. The hot reloading allows you to do that and instantly see your changes come across in the browser. For the most part anyway (sometimes you DO have to restart your server, so please keep that in mind).
I usually take a moment to clean up the scaffolded code. IMO, we should always keep our code base clean and avoid having too many files if we don’t need them. I also get rid of some of the css and test files, as well as the svg file with the spinning React logo. I suggest that you do the same. As a personal preference, I also change the suffix on the Appcomponent to .jsx.
Your folder and file structure should look something like this:

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
│   ├── index.js
│   └── serviceWorker.js
└── yarn.lock
```

You will note a few errors in your browser as you delete the files. That is, of course, caused by the imports in your index.js and App.jsx. Make sure that none of the deleted files are being imported in any of these two files. At this stage, I usually also clean up the returned jsx by the App component.

```
// src/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import * as serviceWorker from './serviceWorker';
ReactDOM.render(<App />, document.getElementById('root'));
serviceWorker.unregister();
// src/App.jsx
import React from 'react';
const App = () => { {
  return (
    <>
      <h1>
        Hello World
      </h1>
    </>
  );
}
export default App;
```
At this stage, we have a “Hello World” application, up and running. 

Start your application from your command line (terminal)

```
$ yarn start
```

So far, so good.
