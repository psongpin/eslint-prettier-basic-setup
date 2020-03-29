## Basic Linting and Formatter Setup on CRA

This repo documents the basic setup for ESLint with Airbnb config, Prettier, Husky, Lint-Staged with React on CRA.

### Create React App

Follow project installation guide: https://create-react-app.dev/docs/getting-started/

### ESLint

- Run `npm install eslint --save-dev` to install ESLint to local project folder.
- Run `npx eslint --init` or `./node_modules/.bin/eslint --init` to initialize eslint setup.
- During the initialization, it will prompt you to answer some questions essential to the need of the project. Here are the answers that I use for the setup (answers in bold):
  
  - How would you like to use ESLint? **To check syntax, find problems, and enforce code style**
  - What type of modules does your project use? **JavaScript modules (import/export)**
  - Which framework does your project use? **React**
  - Does your project use TypeScript? **No**
  - Where does your code run? **Browser**
  - How would you like to define a style for your project? **Use a popular style guide**
  - Which style guide do you want to follow? **Airbnb (https://github.com/airbnb/javascript)**
  - What format do you want your config file to be in? **JSON**

- After answering the question, It will prompt you to install some missing dependency.
  
  - Would you like to install them now with npm? **Yes**
  
- It will generate a `.eslintrc.json` file with some initial configs. I prefer to rename my file with `.eslintrc` as preference.
- Add `"airbnb/hooks"` in `"extends"` property in `.eslintrc.json/.eslintrc`to make react hooks linting rules work.
- Add this rule in the `.eslintrc.json/.eslintrc` file. This will allow React JSX format in JS files:
```
"rules": {
  "react/jsx-filename-extension": [
    1,
    {
      "extensions": [".js", ".jsx"]
    }
  ]
}
```
- Any additional rule overrides to the linter shall be added to the "rules" property.
- in `package.json`, add `"lint": "eslint 'src/**/*.{js,jsx}' --fix"` just incase you want to do linting manually across the codebase.
