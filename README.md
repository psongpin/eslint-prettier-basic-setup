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
- Add `"airbnb/hooks"` in `extends` property in `.eslintrc.json/.eslintrc`to make react hooks linting rules work.
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
- Any additional rule overrides to the linter shall be added to the `rules` property.
- in `package.json`, add the following `scripts` just incase you want to do linting manually across the codebase:
```
"lint": "eslint 'src/**/*.{js,jsx}'",
"lint:fix": "eslint 'src/**/*.{js,jsx}' --fix"
```


### Prettier

- Install the following packages as dev dependencies: `npm i prettier eslint-config-prettier eslint-plugin-prettier --save-dev`
- Update `extends` in your .eslintrc file as follows. Add `plugin:prettier/recommended`:
```
"extends": [
  "plugin:react/recommended",
  "airbnb",
  "airbnb/hooks",
  "plugin:prettier/recommended"
],
```
- If you don’t like the default Prettier configuration, you can create a `.prettierrc` file. Here's my configuration:
```
{
  "arrowParens": "always",
  "bracketSpacing": true,
  "jsxBracketSameLine": false,
  "jsxSingleQuote": false,
  "printWidth": 80,
  "semi": false,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "useTabs": false
}
```
- Add the following `script` in `package.json` in case you want to manually format files accross the codebase: `"format": "prettier --write 'src/**/*.{js,jsx,css,scss}'"`.


### Husky

- Add husky to dev dependencies `npm i husky --save-dev`.
- Create `.huskyrc` file in the root of the project. This is where all husky configs will be placed.
- Add the following in the `.huskyrc`:
```
{
  "hooks": {
    "pre-commit": "lint-staged"
  }
}
```
- This will allow us to do a script command before doing a commit. the `lint-staged` script will contain the commands that should be done before commit. Check the next section for setting up lint-staged.


### Lint-Staged

- Add lint-staged to dev dependencies `npm i lint-staged --save-dev`.
- Create `.lintstagedrc` file in the root of the project. This is where all lint-staged configs will be placed.
- Add the following in the `.lintstagedrc`:
```
{
  "*.js": ["eslint --fix"],
  "**/*.+(js|jsx|json|css)": ["prettier --write", "git add"]
}
```
- This will lint the js files, format the js, jsx, json or css files then re-add it before doing a git commit.
