##### Last updated 2019.08.27

# Basic Setup

I use Linux (Ubuntu) and Bash for development. Your experience may require different instructions.

These instructions are mostly for personal use: the very basics of getting a React project set up. I have brief explanations if a curious new developer comes across this, but if you want more explanation of the steps (especially the code), there are many tutorials out there (a couple of which I used for this).

## Prerequisites

Install [Node](https://nodejs.org/) and npm (I use the latest LTS version of Node; npm will be installed with Node)

[I used NVM for my latest install](https://hackernoon.com/how-to-install-node-js-on-ubuntu-16-04-18-04-using-nvm-node-version-manager-668a7166b854) since I have a history of projects that use different versions.

[I used to install from source with these instructions](https://gist.github.com/toastynerd/d3e563522977f6750c32)—make sure you update the version number! (These instructions also show how to check if you have Node and npm and how to uninstall them.) The advantage of compiling from source is not having to use root access (`sudo`) to install global packages.

## Step 0: Initialize the Project

Create a folder for the project (for example, in Bash: `mkdir new-react-project`, but give it a meaningful name).

##### In Bash / Command Line

Enter folder: `cd new-react-project`

Initialize as npm project: `npm init -y` (This creates a file called [package.json](https://docs.npmjs.com/files/package.json) for the project, which is needed for Node/npm development.) You can forego "-y" if you know what you're doing or are a little more interested in exploring the setup of an npm project.

* A file called package-lock.json is also created, which is a relatively recent npm addition. It should not be deleted and should be uploaded to the repo / tracked by source control.

## 1. Install React

`npm install --save react react-dom`

## 2. Install Babel

`npm i --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader`

### 2.1. Set Up a Babel Config File

In the project's root folder, create a file named **.babelrc**:

```javascript
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}
```

## 3. Install Webpack

`npm i -D webpack webpack-dev-server html-webpack-plugin`

### 3.1. Set Up a Webpack Config File

In the project's root folder, create a file named **webpack.config.js**:

```javascript
var HTMLWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: __dirname + '/app/app.js',

  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: 'babel-loader'
      }
    ]
  },

  output: {
    filename: 'bundle.js',
    path: __dirname + '/build'
  },

  plugins: [
    new HTMLWebpackPlugin({
      template: __dirname + '/app/index.html',
      filename: 'index.html',
      inject: 'body'
    })
  ],

  devtool: 'inline-source-map'
};
```

## 4. Create Basic Files for React Website

### 4.1. Create App Folders

Using Bash in the root of your project: `mkdir -p app/components/App`

### 4.2. Create the HTML File

In the **app** folder, create a file called **index.html** like the one in this project.

### 4.3. Create the React Files

In the **app** folder, create a file called **app.js** like the one in this project.

In the **app/components/App** folder, create a file called **index.js** like the one in this project.

* For my project, I put the **App** folder in a folder called **containers**, because I'm planning to expand this project to use Redux and become much larger. If you're just getting started with React, you probably just want to begin with a **components** folder (_make sure your import in **app.js** references the **index.js** file from the correct folder_).

## 5. Give npm Ways to Run Dev Server and Build Bundle

Replace `"scripts"` lines in `package.json` with `build` and `start` commands for the most basic setup:

```javascript
  "scripts": {
    "build": "webpack",
    "start": "webpack-dev-server --mode development"
  },
```

## 7. Running and Building

Run the dev server by typing `npm start` into the command line. View the site at localhost:8080 to make sure it works.

Build the project using `npm run build`. There will likely be warnings about file-size limits. This is due to the sourcemap being built in the bundle (I will handle the warnings later as I expand my project). View the site by opening the **index.html** file _from the build folder_ to make sure the build works.

## Postrequisites

### Add a README

In the root folder, create a file called **README.md**. In it, explain the purpose of your project and how to use it (install instructions, library functions, setup for development, etc.).

### Add source control.

I use git: `git init`. Then add "node_modules" and "build" _on separate lines_ to a file called **.gitignore** in the project's root folder so they don't get tracked and unnecessarily uploaded to the repository.

Check your status to make sure the correct files are being tracked: `git status`.

Add files to the project and commit them: `git add .` then `git commit -m "Project initialized, and basics in place for developing in React."`.

Upload to online repo if desired.

##

#### Next Steps for Expanding Setup

(This will be a separate repo.)

* Add styling
* Introduce ES6
