# Javascript Fast Track :rocket:

The objective of this project is offer a simple and fast overview about modern Javascript architecture.

**Requirements:**

 - Ubuntu Desktop 20.04 LTS
 - Basic knowledge about Linux commands
 - Basic knowledge about programming

**Source Code**

The source code for this project can be found at: https://github.com/ricardomaia/myproject

# Roadmap

*   [ ] [Install Node](#install-node)
*   [ ] Install Git
*   [ ] Install Visual Studio Code and some useful extensions
*   [ ] Create and clone a GitHub repository
*   [ ] Create a React project (front-end)
*   [ ] Install Express and configure dev scripts
*   [ ] Create a back-end service
*   [ ] Create a simple client interface to consumes the back-end API and shows our data
*   [ ] Commit and push changes to GitHub repository
*   [ ] Deploy our application deploy to heroku from GitHub

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

If you get something like `v14.15.4` good job!

## Install Git

Install Git is easy as any other package on Ubuntu. There's no rocket science here!

```console
sudo apt install git
```

## Install Visual Studio Code and some amazing extensions

To install VSCode from original Microsoft sources, first you need add the repository address to apt source list and trust in their public key.

Commands output below are supressed by `[...]`.

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

Finally open Visual Studio code just typing `code` on terminal or search for appropriate application icon in the Applicatons List.

![](https://i.imgur.com/En9Q9eo.png)

Now, look on the left side menu. Click on the ![](https://i.imgur.com/XjAbULo.png) icon and type the name of extension to install. Finally click in the blue button labeled "install". Repeat the process for each desired extension.

![](https://i.imgur.com/wli6nMP.png)

### Recommended Extensions

*   Git Extension Pack (Don Jayamanne)
*   Formatting Toggle (tombonnike)(
*   Babel JavaScript (Michael McDermott)
*   file-icons (file-icons)
*   Material Icon Theme (Philipp Kief)
*   npm Intellisense (Christian Kohler)
*   Path Intellisense (Christian Kohler)
*   Prettier - Code formatter (Prettier)
*   Bracket Pair Colorizer 2 (CoenraadS)
*   DotENV (mikestead)

That's all for now. Close Visual Studio Code.

Let's take a look in our list...

*   [x] Install Node
*   [x] Install Git
*   [x] Install Visual Studio Code and some useful extensions
*   [ ] Create and clone a GitHub repository
*   [ ] Create a React project (front-end)
*   [ ] Install Express and configure dev scripts
*   [ ] Create a back-end service
*   [ ] Create a simple client interface to consumes the back-end API and shows our data
*   [ ] Commit and push changes to GitHub repository
*   [ ] Deploy our application deploy to heroku from GitHub

Ok! Next step... Create and clone your GitHub repository. Come on!

## Create and clone a GitHub repository

If you don't have an account yet, create one! Go to https://github.com/, click on the "Sign up" button. Fill and submit all form informations, so confirm your email on the message send by GitHub. After all regular steps to create your account Sign in.

Now click on the button "Create repository".

![](https://i.imgur.com/poNKofC.png)

Now you will now see your repository page. Notice a green button with the text "Code". Click to display the drop-down menu and copy the address inside input box.

![](https://i.imgur.com/XWY0397.png)

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

![](https://i.imgur.com/Jjtzc0Y.png)

Open your browser to http://localhost:3000. You will see something like this!

![](https://i.imgur.com/AhdERMX.png)

Open a new terminal ("Terminal" > "New Terminal"), create the backend directory, change to new directory and initialize a node project.

Just type \[Enter\] to all questions and answer "yes" at the end.

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
npm install morgan --save
npm install body-parser --save
npm install nodemon --save-dev
npm install cors --save-dev
npm install reload --save-dev
npm install dotenv --save-dev
```

At the end your `package.json` file must be like this:

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
    "body-parser": "^1.19.0",
    "express": "^4.17.1",
    "morgan": "^1.10.0"
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


const app = express()
app.use(logger('dev'))
app.use(bodyParser.json())
app.use(express.urlencoded({ extended: false }))

const corsOptions = {
  origin: '*',
  optionsSuccessStatus: 200, // some legacy browsers (IE11, various SmartTVs) choke on 204
}

app.use(cors(corsOptions))
app.set('port', process.env.PORT || 5000)
app.use(express.static('public'))


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
      'Reload could not start, could not start server',
      err
    )
  })
var server = http.createServer(app)

/**
 * https://next.json-generator.com/Nk6OQ_EAt
 */
app.get('/hello', (req, res) => {
    res.send(
[
  {
    "_id": "5ffb845d98c8f8d41b556b19",
    "index": 0,
    "guid": "8e09d117-8b2a-435b-8bf1-a5a33436d263",
    "isActive": false,
    "picture": "https://via.placeholder.com/300x400",
    "age": 33,
    "name": {
      "first": "Byrd",
      "last": "Robinson"
    },
    "email": "byrd.robinson@undefined.io",
    "phone": "+1 (934) 467-2967",
    "address": "656 Cooper Street, Cherokee, Palau, 1968",
    "registered": "Sunday, February 23, 2020 5:20 PM"
  },
  {
    "_id": "5ffb845d24ca5e847606f736",
    "index": 1,
    "guid": "9ee801d3-d8c9-4882-8b59-66d95841b18f",
    "isActive": false,
    "picture": "https://via.placeholder.com/300x400",
    "age": 24,
    "name": {
      "first": "Watson",
      "last": "Bryant"
    },
    "email": "watson.bryant@undefined.com",
    "phone": "+1 (886) 509-3317",
    "address": "912 Bouck Court, Katonah, Missouri, 4984",
    "registered": "Wednesday, July 11, 2018 10:24 AM"
  },
  {
    "_id": "5ffb845db30ce4b4afe8d63a",
    "index": 2,
    "guid": "418ff494-f926-450a-a560-bdc6c31bce97",
    "isActive": false,
    "picture": "https://via.placeholder.com/300x400",
    "age": 22,
    "name": {
      "first": "Gracie",
      "last": "Kelly"
    },
    "email": "gracie.kelly@undefined.biz",
    "phone": "+1 (952) 482-3165",
    "address": "549 Whitwell Place, Albrightsville, Minnesota, 2925",
    "registered": "Sunday, July 30, 2017 4:52 PM"
  },
  {
    "_id": "5ffb845d6be170e285d1fe3f",
    "index": 3,
    "guid": "8d5b9a6f-5cb6-423e-bc44-29040b963770",
    "isActive": false,
    "picture": "https://via.placeholder.com/300x400",
    "age": 36,
    "name": {
      "first": "Shelia",
      "last": "Frazier"
    },
    "email": "shelia.frazier@undefined.biz",
    "phone": "+1 (825) 531-3288",
    "address": "145 Hemlock Street, Courtland, South Dakota, 8010",
    "registered": "Tuesday, April 30, 2019 11:32 AM"
  },
  {
    "_id": "5ffb845d8e839db7a3920e50",
    "index": 4,
    "guid": "29e18aad-311e-432f-8d91-2f30c144b39a",
    "isActive": false,
    "picture": "https://via.placeholder.com/300x400",
    "age": 31,
    "name": {
      "first": "Hamilton",
      "last": "Farrell"
    },
    "email": "hamilton.farrell@undefined.org",
    "phone": "+1 (948) 488-2849",
    "address": "325 Crooke Avenue, Barstow, Kansas, 802",
    "registered": "Tuesday, August 6, 2019 4:02 AM"
  },
  {
    "_id": "5ffb845db99bcb012e8f43ef",
    "index": 5,
    "guid": "d23c178f-2117-47de-a4d2-d4129a0c5d0b",
    "isActive": true,
    "picture": "https://via.placeholder.com/300x400",
    "age": 35,
    "name": {
      "first": "Hilary",
      "last": "Head"
    },
    "email": "hilary.head@undefined.tv",
    "phone": "+1 (878) 465-3689",
    "address": "572 Sumner Place, Albany, Pennsylvania, 6618",
    "registered": "Monday, April 13, 2020 9:27 PM"
  },
  {
    "_id": "5ffb845d04a1b4329d893ca8",
    "index": 6,
    "guid": "f99fada0-75c0-44d1-a888-385bf2a8a266",
    "isActive": false,
    "picture": "https://via.placeholder.com/300x400",
    "age": 30,
    "name": {
      "first": "Lara",
      "last": "Keith"
    },
    "email": "lara.keith@undefined.net",
    "phone": "+1 (981) 437-2514",
    "address": "756 Conduit Boulevard, Grimsley, Guam, 9438",
    "registered": "Monday, May 11, 2020 4:37 AM"
  },
  {
    "_id": "5ffb845d9403215ee2145d4b",
    "index": 7,
    "guid": "949024eb-227a-405d-89be-5f01588dd519",
    "isActive": false,
    "picture": "https://via.placeholder.com/300x400",
    "age": 22,
    "name": {
      "first": "Nanette",
      "last": "Gentry"
    },
    "email": "nanette.gentry@undefined.ca",
    "phone": "+1 (986) 430-3787",
    "address": "478 Campus Road, Felt, Vermont, 3395",
    "registered": "Thursday, March 12, 2015 7:57 AM"
  }
])
  })
```

One more time, let's take a look in our list...

*   [x] Install Node
*   [x] Install Git
*   [x] Install Visual Studio Code and some useful extensions
*   [x] Create and clone a GitHub repository
*   [x] Create a React project (front-end)
*   [x] Install Express and configure dev scripts
*   [x] Create a back-end service
*   [ ] Create a simple client interface to consumes the back-end API and shows our data
*   [ ] Commit and push changes to GitHub repository
*   [ ] Deploy our application deploy to heroku from GitHub

## Commit and push changes to GitHub repository

Create `.gitignore` file on root of backend directory to ignore node\_modules.

```
node_modules
```

Click on **Source Control** icon ![](https://i.imgur.com/f5LYKkL.png) and commit to local repository with a message.

![](https://i.imgur.com/U22Ctcp.png)

Push to remote repository on GitHub

![](https://i.imgur.com/MgODr9G.png)

# Extras

## SSH and Surge.sh deploy

In this scenario we have two build flows, production and development, based into master and develop branches respectively.

The production flow deploys our application to a VPS server using SSH. The development deploys to Surge.sh, a service to web publishing.

### Surge.sh

Install surge package in your computer and create an account.n 

```console
npm install --global surge
surge
```
Create a Surge.sh token to use in GitHub CI/CD workflow as secret. Save the generated token for later.

```console
surge token
```

### Add a deployer user

```console
adduser deployer
```

### Add permissions to destination directory

```console
chmod -R 775 destination_directory
chown -R root.deployer destination_directory
```

### Create a SSH keys on your server

Use NO PASSPHRASE.

```console
cd /home/deployer
ssh-keygen -m PEM -t rsa -b 4096 -C "deployer@yourhost.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/deployer/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/deployer/.ssh/id_rsa
Your public key has been saved in /home/deployer/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:QauskbwD7z2JgXM44HcrNYI4LpVdZYUst9NAPm0SFtk deployer@yourhost.com
The key's randomart image is:
+---[RSA 4096]----+
|   .* ..+o+..**  |
|  .. . o.= .+o E |
|..      = o.. o  |
|     +..+ o . + .|
|     +o*.*+o S . |
|  ..*+*o.        |
|    **o          |
|       ..o .     |
|    .+..         |
+----[SHA256]-----+

```

### Copy the public key to authorized_keys file

```console
cd /home/deployer/.ssh
cat id_rsa.pub >> authorized_keys
```

### Backup your private key to use with GitHub actions

```console
cd /home/deployer/.ssh
cat id_rsa
```

You will see something like this...

```
-----BEGIN RSA PRIVATE KEY-----
MIIJKQIBAAKCAgEAldqG7aAxG2V7JrD+52YTn+WmZsPUahOaYPtgz+LCKtgKU5bJ
kXGtcEuVrY0eLk1b6+8DUwRPe952l7uYCAE7n4QYD8vvGnVW/2Mw/xELZrcRbYhT
HcTMbDzR7f51eUb1tmukJ/Xc/uvOd9pCbtEOQQkhHR7V+mmquqeUEDyZkXkrL/mT
[...]
rratHV/ZVyMEJtIddpgPTHVLl4LWO3gonIE0aVUcpPTra5YvTeDEoIsfqiPX5pFr
MlIkfBfO8do/cYYoN0F1gQgfDFuja1JNvM/R+nELMGlxucyPexo5Gak+nhGvCI3l
GZtLniFVV/LJSqX8szQuO+pafpMMfhf+lgeir9ug5TTZLRn9yE8JUi8MlUqq2sch
-----END RSA PRIVATE KEY-----
```

### Set GitHub repository secrets

Go to https://github.com/[:your_username]/[:repository]/settings/secrets/actions

 - DEPLOY_KEY: Your SSH private key
 - DEPLOY_HOST: VPS IP address or name
 - DEPLOY_USER: Deployer username
 - DEPLOY_TARGET: Destination folder for build files
 - SURGE_TOKEN: Your Surge.sh token

<img src="https://i.imgur.com/47OEjil.png">

### Add a GitHub action file into your repository ```.github/workflows/deploy.yaml```

```deploy.yaml
name: Node CI

on:
  push:
    branches:
      - master
      - develop

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v1

      - name: Install Node.js
        uses: actions/setup-node@v1
        with:
          node-version: "10.x"

      - name: Install npm dependencies
        run: npm install

      - name: Run build task
        run: npx next build && npx next export

      ## Build & Deploy Dev
      - name: Build & Deploy Dev
        if: github.ref == 'refs/heads/develop'
        run: |
          npm install -g surge
          surge ./out https://your-custom-url.surge.sh/ --token ${{secrets.SURGE_TOKEN}}

      ## Build & Deploy Production
      - name: Build & Deploy Production
        if: github.ref == 'refs/heads/master'
        uses: easingthemes/ssh-deploy@v2.1.5
        env:
          SSH_PRIVATE_KEY: ${{ secrets.DEPLOY_KEY }}
          ARGS: "-rltgoDzvO --delete"
          SOURCE: "out/"
          REMOTE_HOST: ${{ secrets.DEPLOY_HOST }}
          REMOTE_USER: ${{ secrets.DEPLOY_USER }}
          TARGET: ${{ secrets.DEPLOY_TARGET }}
```

# Next Steps

* Separate and each service into a container
* Use a reverse proxy like NGINX in front of Express
* Use Docker Compose to set up your production environment
* Set NGINX upstream module to provide loadbalance
* Use a process manager for Node like [StrongLoop PM](http://strong-pm.io/)
* Manual scaling with Docker Swarm
* Auto scaling with Kubernetes (Horizontal Pod Autoscaler)

# Quick References

*   [Git Cheat Sheets](https://training.github.com/)
