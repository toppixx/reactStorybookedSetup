This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br />
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br />
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br />
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br />
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br />
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).


//install the npx library (binary execution for react creation tools)
npm install -g npx 

//create a new react project
npx create-react-app project** --typescript

    //or by an existing project
    npm install --save typescript @types/node @types/react @types/react-dom @types/jest

//install storybook
//short but not very kind
npx sb init
//long but more specific (z.B. using storybook only in developing not for release)
//https://medium.com/@dandobusiness/setting-up-a-react-typescript-storybook-project-5e4e9f540568
npm i -D @storybook/react
   //create new Folder/File Structur
   .storybook
    - addons.js
    - config.js 
    - tsconfig.json
    - webpack.config.js

<<<<------------------------------------>>>>>>
   //config.js

   import { configure } from '@storybook/react';

   const req = require.context('../src/components', true, /.stories.tsx$/);

   function loadStories() {

     req.keys().forEach(req);

   }

   configure(loadStories, module);

<<<<------------------------------------>>>>>>
//tsconfig.json
{
  "compilerOptions": {
    "baseUrl": "./",
    "allowSyntheticDefaultImports": true,
    "module": "es2015",
    "target": "es5",
    "lib": ["es6", "dom"],
    "sourceMap": true,
    "allowJs": false,
    "jsx": "react",
    "moduleResolution": "node",
    "rootDir": "../",
    "outDir": "dist",
    "noImplicitReturns": true,
    "noImplicitThis": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "declaration": true
  },
  "include": [
    "src/**/*"
  ],
  "exclude": [
    "node_modules",
    "build",
    "dist",
    "scripts",
    "acceptance-tests",
    "webpack",
    "jest",
    "src/setupTests.ts",
    "**/*/*.test.ts",
    "examples"
  ]
}


<<<<------------------------------------>>>>>>
//further install packages
npm i -D awesome-typescript-loader
npm i -D react-docgen-typescript-loader
npm i -D react-docgen-typescript-webpack-plugin

<<<<------------------------------------>>>>>>
//webpack.config.js
const path = require("path");
const SRC_PATH = path.join(__dirname, '../src');
const STORIES_PATH = path.join(__dirname, '../stories');
//dont need stories path if you have your stories inside your //components folder
module.exports = ({config}) => {
  config.module.rules.push({
    test: /\.(ts|tsx)$/,
    include: [SRC_PATH, STORIES_PATH],
      use: [
        {
          loader: require.resolve(’awesome-typescript-loader’),
          options: {
            configFileName: './.storybook/tsconfig.json'
          }
        },
        { loader: require.resolve(’react-docgen-typescript-loader’) }
      ]
  });
  config.resolve.extensions.push(’.ts’, '.tsx’);
  return config;
};
<<<<------------------------------------>>>>>>


//Inside your package.json file underneath the other scripts include the following:
//under scripts
"storybook": "start-storybook -p 9001 -c .storybook"


cd project**
npm run 