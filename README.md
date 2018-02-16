# Vue CLI -- Scratchpad Notes
Notes (last updated: 2/15/2018)

### Project Goal:
Create a project using Vue.js CLI, webpack, bootstrap v4, git for version control, and deploy to github pages

### Links:

[Vue.js 2.x Guide](https://vuejs.org/v2/guide/installation.html#CLI)

[Vue.js webpack template](https://vuejs-templates.github.io/webpack/)

[Bootstrap v4 webpack](https://getbootstrap.com/docs/4.0/getting-started/webpack/)

[webpack](https://webpack.js.org/concepts/)

## Process:

### 1) Create new GitHub repo, don't create README yet, don't clone

### 2) Create new Vue.js project using the webpack template
1) `$ vue init webpack <project-title>` and then follow prompts
2) `$ cd <project-title>` (enter newly created directory)
3) go to `/config/index.js`, find the `build` object, and change `assetsPublicPath:`'s value to `'./`
4) back in root directory, `npm run build` to bundle project into newly created `dist/` folder

### 3) Initialize git repo
1) `git init`
2) `git add .`
3) `git commit -m "Initial commit"`
4) `git remote add origin <github's remote ssh/https link>`
5) `git push -u origin master`

### 4) Create branch (for GitHub pages) and deploy from production code directory
(FYI - the `dist/` folder is `.gitignore`'d by default... use this to our advantage)
1) `cd dist`
2) `git init`
3) `git add .`
4) `git commit -m "Initial commit"`
5) `git remote add origin <github's remote ssh/https link>`
6) `git push --force origin master:gh-pages`
**Check GitHub pages link for successful deployment of Vue.js default theme content**
