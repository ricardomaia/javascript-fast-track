# Javascript Fast Track :rocket:

The objective of this project is offer a simple and fast overview about modern Javascript ecosystem.

**Requirements:**

 - Ubuntu Desktop 20.04 LTS
 - Basic knowledge about Linux commands
 - Basic knowledge about programming

# Roadmap

- [ ] [Install Node](#install-node)
- [ ] Install Git
- [ ] Install Visual Studio Code and some useful extensions
- [ ] Create and clone a GitHub repository
- [ ] Create a React project (front-end)
- [ ] Install Express and configure dev scripts
- [ ] Install MongoDB and create a simple database
- [ ] Create a back-end service
- [ ] Create a simple client interface to consumes the back-end API and shows our data

## Install Node

```console
curl -sL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs
```

After installation verify node version to check if everything is ok.

```console
node -v
v14.15.4
```

If you get something like ```v14.15.4``` good job!

## Install Git

Install Git is easy as any other package on Ubuntu. There's no rocket science here!

```console
sudo apt install git
```

## Install Visual Studio Code and some amazing extensions

To install VSCode from original Microsoft sources, first you need add the repository address to apt source list and trust in their public key. 

Commands output below are supressed by ```[...]```.

```console
sudo apt update
[...]
sudo apt install software-properties-common apt-transport-https wget
[...]
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add --
[...]
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
[...]
sudo apt install code
```

Finally open Visual Studio code just typing ```code``` on terminal or search for appropriate application icon in the Applicatons List.

<img src="https://i.imgur.com/En9Q9eo.png" />

Now, look on the left side menu. Click on the <img src="https://i.imgur.com/XjAbULo.png" /> icon and type the name of extension to install. Finally click in the blue button labeled "install". Repeat the process for each desired extension.

<img src="https://i.imgur.com/wli6nMP.png" />

### Recommended Extensions
 - Git Extension Pack (Don Jayamanne)
 - Formatting Toggle (tombonnike)(
 - Babel JavaScript (Michael McDermott)
 - file-icons (file-icons)
 - Material Icon Theme (Philipp Kief)
 - npm Intellisense (Christian Kohler)
 - Path Intellisense (Christian Kohler)
 - Prettier - Code formatter (Prettier)
 - Bracket Pair Colorizer 2 (CoenraadS)
 - DotENV (mikestead)
 
That's all for now. Close Visual Studio Code.

Let's take a look in our list...

- [x] Install Node
- [x] Install Git
- [x] Install Visual Studio Code and some useful extensions
- [ ] Create and clone a GitHub repository
- [ ] Create a React project (front-end)
- [ ] Install Express and configure dev scripts
- [ ] Install MongoDB and create a simple database
- [ ] Create a back-end service
- [ ] Create a simple client interface to consumes the back-end API and shows our data

Ok! Next step... Create and clone your GitHub repository. Come on!

## Create and clone a GitHub repository

If you don't have an account yet, create one! Go to https://github.com/, click on the "Sign up" button. Fill and submit all form informations, so confirm your email on the message send by GitHub. After all regular steps to create your account Sign in.

Now click on the button "Create repository".

<img src="https://i.imgur.com/poNKofC.png" />

Now you will now see your repository page. Notice a green button with the text "Code". Click to display the drop-down menu and copy the address inside input box.

<img src="https://i.imgur.com/XWY0397.png" />

```console
cd ~
mkdir github
cd github
git clone https://github.com/[your-username]/myproject.git
```

A good idea is set globally your name and email to use with Git.

```console
git config --global user.name "John Doe"
git config --global user.email doe@exemple.com
```

## Create a React project

In our project we will use two directories, "frontend" and "backend". It will make sense later!

Next we are going to create our "React" project. Then open Visual Studio Code on current directory.

```console
npx create-react-app frontend
code ./
```
You shold see our project directory structure into Visual Studio Code. Now open a new terminal on top menu "Terminal" > "New Terminal" and enter the following commands:

```console
cd frontend
npm start
```

<img src="https://i.imgur.com/Jjtzc0Y.png" />

Open your browser to http://localhost:3000. You will see something like this!

<img src="https://i.imgur.com/AhdERMX.png" />

Open a new terminal ("Terminal" > "New Terminal"), create the backend directory, change to new directory and initialize a node project.

Just type [Enter] to all questions and answer "yes" at the end.

```console
mkdir backend
cd backend
npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (backend) 
version: (1.0.0) 
description: 
entry point: (index.js) 
test command: 
git repository: 
keywords: 
author: 
license: (ISC) 
About to write to /home/brainfork/github/myproject/backend/package.json:

{
  "name": "backend",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}

Is this OK? (yes) yes
```

Install **express** package as dependency in our project. The others packages, like nodemon will be used only at development time.

```console
npm install express --save
npm install nodemon --save-dev
npm install cors --save-dev
npm install reload --save-dev
npm install dotenv --save-dev
```

At the end your ```package.json``` file must be like this:

```json
{
  "name": "backend",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "cors": "^2.8.5",
    "dotenv": "^8.2.0",
    "nodemon": "^2.0.7",
    "reload": "^3.1.1"
  }
}
```

Now on VSCode create the entrypoint file to the backend (index.js).

```javascript
const express = require('express')
const http = require('http')
const reload = require('reload')
const bodyParser = require('body-parser')
const logger = require('morgan')
const cors = require('cors')
const dotenv = require('dotenv')

// Environment Configurations
dotenv.config({ path: `${__dirname} /../.env` })
const env = process.env.NODE_ENV

// Routes
const importChats = require('./routes/import-chats')

const app = express()
app.use(logger('dev'))
app.use(bodyParser.json())
app.use(express.urlencoded({ extended: false }))

const corsOptions = {
  origin: '*',
  optionsSuccessStatus: 200, // some legacy browsers (IE11, various SmartTVs) choke on 204
}

app.use(cors(corsOptions))
app.set('port', process.env.PORT || 3000)
app.use(express.static('public'))

// Using routes
app.use('/import', importChats)

// Reload code here
reload(app)
  .then(function (reloadReturned) {
    // reloadReturned is documented in the returns API in the README

    // Reload started, start web server
    server.listen(app.get('port'), function () {
      console.log('Web server listening on port ' + app.get('port'))
    })
  })
  .catch(function (err) {
    console.error(
      'Reload could not start, could not start server/sample app',
      err
    )
  })
var server = http.createServer(app)

/**
 *
 */
app.get('/foo', (req, res) => {
  res.send('foo')
```

# Next Steps

- Separate and each service into a container
- Use a reverse proxy like Nginx in front of Express
- Use a process manager for Node like [StrongLoop PM](http://strong-pm.io/)

# Quick References
 - [Git Cheat Sheets](https://training.github.com/)
