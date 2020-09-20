# JS-WEBPACK

mkdir webpacktut && cd webpacktut

npm init -y // Creates the package .json

npm install -D webpack webpack-cli   // installs webpack and webpack-cli

open vs code 

-----------------------------------------------------------------------

open package.json and remove test -->
make it build value webpack

"scripts": {
    "dev": "webpack --mode development",
    "build": "webpack --mode production"
  },

Now just npm run build nothing will happen it will throw an error no src folder

So create src folder in root and add a index.js file

now run npm run build

nothing much will happen but it creates a folder dist

now create a bro.js file and import it in index.js
like 

src/bro.js

const bro = (greeting) => {
    return `${greeting} Bro!!!`;
}

src/index.js

import { bro } from './bro'

console.log(bro('dude'));

now create a src/index.html

in html add index.js and run ... it will not work
error saying syntax error .. 

webpack 4.0 doesnt understand html..

now we create config file

in root webpack.config.js // dont write yet
then 


 root webpack.config.js
const path = require('path');
module.exports = {
    entry: ['./src/js/index.js'],
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'js/bundle.js'
    },
    mode: 'development'
    
};


 now add dev server (to auto build the app like angular :))
 
 npm install webpack-dev-server --save-dev or npm install -D webpack-dev-server 
 root webpack.config.js below add this object
 devServer: {
        contentBase: './dist'
},

now add npm script in package.json
 "scripts": {
    "dev": "webpack --mode development",
    "build": "webpack --mode production",
    "start": "webpack-dev-server --mode development --open"
  },
  
 then run if u change also it automatically works
 
 npm install -D html-webpack-plugin //html-loader
 
 then add 
 
 root/webpack.config.js
 at top 
const HtmlWebpackPlugin = require('html-webpack-plugin')

and then add plugins below dev-serve object
 plugins: [
        new HtmlWebpackPlugin({
            filename: 'index.html',
            template: './src/index.html'
        })
    ],
 
 NOw stop and start the server
 
 it works, But u cant see the file in dist folder coz the dev server will not save it to disk but loads
 
 
 bebel :)
 
 for babel install
 npm install --save-dev @babel/core @babel/preset-env babel-loader npm install --save core-js@3 regenerator-runtime
 
 
 add in webpack.config.js
 
 module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                 use: {
                     loader: 'babel-loader'
                 }
            }
        ]
    }
 


create  a .babelrc file

{
    "presets": [
        ["@babel/env", {
            "useBuiltIns": "usage",
            "corejs": "3",
            "targets": {
                "browsers": [
                    "last 5 versions",
                    "ie >= 8"
                ]
            }
        }]
    ]
}
 
 next install bale-polyfill so the es6 which are not there to convert to es5
 
 npm install babel-polyfill --save
 
 and add the entry point in webpack.config.js
  entry: ['babel-polyfill', './src/js/index.js'],
 
 
 

