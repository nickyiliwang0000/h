# Gh-pages deployment with React

## Steps

1. Create a new repository on GitHub.

2. Create a new React app on your computer: 

```bash
npx create-react-app gh-pages-react-app
```

3. Install the gh-pages npm package to your React project:

```bash
npm install gh-pages
```

This will automatically add `gh-pages` to your `package.json` dependencies list:

```bash
"dependencies": {
  "gh-pages": "^2.1.1",
  "react": "^16.12.0",
  "react-dom": "^16.12.0",
  "react-scripts": "3.2.0"
},
  ```

4. Next, we need to manually add some additional data and custom scripts to our `package.json` file. First, we add a new property to the JSON file called `homepage`. The value of this property is the URL for the user/organization or project page:

```
{
  "homepage": "https://username.github.io/repo-name",
  "name": "react-project",
  "version": "0.1.0",
  "private": true,
```

Further down in the `package.json` file, we are going to add two new commands to the `scripts` object, `predeploy` and `deploy`:

```bash
"scripts": {
"predeply": "npm run build",
"deploy": "gh-pages -d build",
"start": "react-scripts start",
},
```

`npm run build` initiates the required process of building your react application to be production-ready. This essentially means that all of your JS and CSS files are minified and bundled into single CSS and JS files to optimize for better browser performance. This process will automatically generate a new folder to your project directory called `build`. This is your deployment-ready folder.

`gh-pages -d build` triggers the publishing of your `build` folder to the `gh-pages` branch on GitHub.

5. Once we have added all of the above code, run `npm run deploy` in your command line to trigger the publishing process. The `predeploy` command will trigger automatically before publishing to GitHub.

Congratulations, your React application is now deployed to GitHub pages. 🚀






