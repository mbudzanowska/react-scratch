## Based on the https://medium.com/@JedaiSaboteur/creating-a-react-app-from-scratch-f3c693b84658

HMR - Hot Module Replacement

Steps to reproduce:
1. npm init
2. create /public and /src folders
3. git init (optional)
4. create .gitignore file
5. add index.html to /public
6. npm install --save-dev @babel/core@7.1.0 @babel/cli@7.1.0 @babel/preset-env@7.1.0 @babel/preset-react@7.0.0

> babel-core is the main babel package — We need this for babel to do any transformations on our code. babel-cli allows you to compile files from the command line. preset-react and preset-env are both presets that transform specific flavors of code — in this case, the env preset allows us to transform ES6+ into more traditional javascript and the react preset does the same, but with JSX instead.

7. create .babelrc file
8. npm install --save-dev webpack@4.19.1 webpack-cli@3.1.1 webpack-dev-server@3.1.8 style-loader@0.23.0 css-loader@1.0.0 babel-loader@8.0.2

> In webpack.config.js - Let’s take a quick walk through this: entry (line 5) tells Webpack where our application starts and where to start bundling our files. The following line lets webpack know we’re working in development mode — This saves us from having to add a mode flag when we run the development server.

> The module object helps define how your exported javascript modules are transformed and which ones are included according to the given array of rules.

> Our first rule is all about transforming our ES6 and JSX syntax. The test and exclude properties are conditions to match file against. In this case, it’ll match anything outside of the node_modules and bower_components directories. Since we’ll be transforming our .js and .jsx files as well, we’ll need to direct Webpack to use Babel. Finally, we specify that we want to use the env preset in options.

> The next rule is for processing CSS. Since we’re not pre-or-post-processing our CSS, we just need to make sure to add style-loader and css-loader to the use property. css-loader requires style-loader in order to work. loader is a shorthand for the use property, when only one loader is being utilized.

> The resolve property allows us to specify which extensions Webpack will resolve — this allows us to import modules without needing to add their extensions.

> The output property tells Webpack where to put our bundled code. The publicPath property specifies what directory the bundle should go in, and also tells webpack-dev-server where to serve files from.

> The publicPath property is a special property that helps us with our dev-server. It specifies the public URL of the the directory — at least as far as webpack-dev-server will know or care. If this is set incorrectly, you’ll get 404’s as the server won’t be serving your files from the correct location!

> We set up webpack-dev-server in the devServer property. This doesn’t require much for our needs — just the location we’re serving static files from (such as our index.html) and the port we want to run the server on. Note that devServer also has a publicPath property. This publicPath tells the server where our bundled code actually is.

> That last bit might have been a little confusing — Pay really close attention here: output.publicPath and devServer.publicPath are different. Read both entries. Twice.

> Finally, since we want to use Hot Module Replacement so we don’t have to constantly refresh to see our changes. All we do for that in terms of this file is instantiate a new instance of the plugin in the plugins property and make sure that we set hotOnly to true in devServer.

9. npm install react@16.5.2  react-dom@16.5.2
10. create index.js file
11. create App.js file
12. create App.css file
13. add start script to package.json - "start": "webpack-dev-server --mode development"
14. npm start (HMR will not work yet, but it should build correctly)
15. npm install react-hot-loader@4.3.11
16. change App.js to support HRM
17. npm start 

18. add build scripts to package.json - "build-dev": "webpack --mode development" and "build-prod": "webpack --mode production",
    (mode --production gives minified output)


> Additional info:
Files never show up in dist directory. webpack-dev-server is actually serving the bundled files from memory — once the server stops, they’re gone.




