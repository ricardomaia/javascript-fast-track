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
- [ ] Install and create a React project (front-end)
- [ ] Install Express and configure dev scripts
- [ ] Install MongoDB and create a simple database
- [ ] Create a backend service

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

## Install Visutal Studio Code

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

Let's see how is our list...

- [x] Install Node
- [x] Install Git
- [x] Install Visual Studio Code and some useful extensions
- [ ] Create and clone a GitHub repository
- [ ] Install and create a React project (front-end)
- [ ] Install Express and configure dev scripts
- [ ] Install MongoDB and create a simple database
- [ ] Create a backend service

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

## Install and create a React project

it will make sense later

# Next Steps

- Separate and each service into a container
- Use a reverse proxy like Nginx in front of Express
- Use a process manager for Node like [StrongLoop PM](http://strong-pm.io/)

# Quick References
 - [Git Cheat Sheets](https://training.github.com/)
