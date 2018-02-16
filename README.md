# Vue CLI -- Scratchpad Notes
Notes (last updated: 2/15/2018)

### Project Goal:
Create a project using Vue.js CLI, webpack, bootstrap v4, git for version control, and deploy to github pages

### Links:

[Vue.js 2.x Guide](https://vuejs.org/v2/guide/installation.html#CLI)

[Vue.js webpack template](https://vuejs-templates.github.io/webpack/)

[Bootstrap v4 webpack](https://getbootstrap.com/docs/4.0/getting-started/webpack/)

[webpack](https://webpack.js.org/concepts/), [webpack configuration](https://webpack.js.org/configuration/), [webpack loaders](https://webpack.js.org/loaders/), [webpack plugins](https://webpack.js.org/plugins/)

## Process:

### 1) Create new GitHub repo, don't create README yet, don't clone

### 2) Create new Vue.js project using the webpack template
1) `$ vue init webpack <project-title>` and then follow prompts
2) `$ cd <project-title>` (enter newly created directory)
3) go to `/config/index.js`, find the `build` object, and change `assetsPublicPath:`'s value to `'./`
4) back in root directory, `$ npm run build` to bundle project into newly created `dist/` folder

### 3) Initialize git repo
1) `$ git init`
2) `$ git add .`
3) `$ git commit -m "Initial commit"`
4) `$ git remote add origin <github's remote ssh/https link>`
5) `$ git push -u origin master`

### 4) Create branch (for GitHub pages) and deploy from production code directory
(FYI - the `dist/` folder is `.gitignore`'d by default... use this to our advantage)
1) `$ cd dist`
2) `$ git init`
3) `$ git add .`
4) `$ git commit -m "Initial commit"`
5) `$ git remote add origin <github's remote ssh/https link>`
6) `$ git push --force origin master:gh-pages`
7) Check GitHub pages link for successful deployment of Vue.js default theme content

### 5) Automate for future build/deployments
Don't do this every time you want to deploy...
```js
function tedious() {
  // deleting the `dist/` folder, `npm build`, then Step 4 from above
} 
```
when you can instead... **SCRIPTIFY IT**

From inside your root's `package.json`, add a script to the `"scripts": {}` object that looks like so:
```
"deploy": "rm -rf dist && npm run build && cd dist && git init && git add . && git commit -m \"Initial commit\" && git remote add origin <github's remote ssh/https link> && git push --force origin master:gh-pages"
```

And now you can create a production build and deploy to your github pages branch with as little as:

`$ npm run deploy`

### 6) Install Bootstrap and its dependencies (jQuery, popper.js, whatever else npm says)
`$ npm install -S boostrap jquery popper.js`

### 7) So... can I start coding yet? (Nope, not yet...) Import/webpack configuration time...

1) Add (aka `require()`, aka `import`) bootstrap and, just to keep it simple, its already-compiled CSS to the "entry point":

In **`src/main.js`**, add this:
```js
import 'bootstrap';
import 'bootstrap/dist/css/bootstrap.min.css';
```

2) webpack can only compute JS by default (not CSS). Since we need webpack handle Bootstraps CSS, we need a webpack "loader"

In your root directory:
```$ npm install -D style-loader css-loader```

In **`build/webpack.base.conf.js`**, add this:

inside of the `module.exports` object, add this object:
```js
{
  test: /\.css$/,
  use: ['style-loader', 'css-loader']
} 
// Aaaaaand now webpack can handle CSS
```

3) Use webpack's [ProvidePlugin](https://webpack.js.org/plugins/provide-plugin/) to automatically load modules (e.g. jQuery and Popper.js) instead of having to `import` or `require` them everywhere

In **`build/webpack.base.conf.js`**, add this:

At the top of the file
```js
const webpack = require('webpack'); //to access built-in plugins
```
and inside the `module.exports` object, just below the `module` and above the `node` properties
```js
plugins: [
    new webpack.ProvidePlugin({
    $: 'jquery',
    jQuery: 'jquery',
    Popper: ['popper.js', 'default'] 
  })
]
```

Questions:
###### 1) How do I `require`/`import` bootstrap/jquery/popper.js in my project?
###### 2) Where should I save my custom css files?
###### 3) How do I link to my custom css files?
###### 4) Where should I save my custom js files?
###### 5) How do I link to my custom js files?
###### 6) Seriously... can I start coding now?

