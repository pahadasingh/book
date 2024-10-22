### Purpose of Webpack
Webpack is a module bundler primarily used for bundling JavaScript files, but it can also handle other types of assets like CSS, images, and HTML. Its primary goal is to manage dependencies, modularize code, and bundle it into a single or multiple output files. This is especially useful for modern web applications that have many interdependent modules.

Webpack performs key tasks like:
- **Module Bundling**: Bundles multiple JavaScript files (and other assets) into a single or multiple bundles.
- **Dependency Management**: Manages dependencies between modules to ensure everything is available when needed.
- **Optimization**: Minifies code, removes dead code, and optimizes assets for production.
- **Development Server**: Provides live reloading, making it easier for developers to test their applications during development.

### Explanation of the Webpack Configuration

#### 1. **Entry and Output**
```js
entry: "./src/index.tsx",
output: {
    filename: "bundle-dev.js",
    path: path.resolve(__dirname, "..", "public"),
    publicPath: "/"
}
```
- **Entry**: Specifies the entry point of the application (i.e., the starting point where Webpack starts bundling). In this case, it's `index.tsx`.
- **Output**: Defines the file name and location where the bundled code will be placed (`bundle-dev.js` in the `public` directory). The `publicPath` is set to `/`, indicating the root of the server will serve the output.

#### 2. **Resolve and ResolveLoader**
```js
resolve: {
    extensions: [".tsx", ".ts", ".js", ".json", ".html"],
    modules: ["node_modules", path.resolve(__dirname, "..", "src")]
},
resolveLoader: {
    modules: ["node_modules"]
}
```
- **Resolve**: This is used to tell Webpack which file extensions to look for while resolving modules. It will automatically resolve `.tsx`, `.ts`, `.js`, `.json`, and `.html` extensions without explicitly specifying them in the `import` statement. It also defines module resolution paths to prioritize the `src` folder and `node_modules`.
- **ResolveLoader**: Specifies where Webpack should look for loaders, in this case, the `node_modules` directory.

#### 3. **DevServer**
```js
devServer: {
    inline: true,
    contentBase: "public/",
    port: 3001,
    proxy: [
        {
            path: "/api/*",
            target: "http://localhost:3001/"
        }
    ],
    historyApiFallback: true
}
```
- **inline**: Enables live reloading, which automatically refreshes the browser when changes are made to the code.
- **contentBase**: Specifies the directory where the static files are located (`public/` in this case).
- **port**: Defines the port for the dev server (`3001`).
- **proxy**: Allows you to proxy API requests. In this configuration, any requests matching `/api/*` will be forwarded to `http://localhost:3001/`.
- **historyApiFallback**: Ensures that all routes serve the `index.html` file, which is important for single-page applications using React Router.

#### 4. **Devtool**
```js
devtool: "source-map"
```
- **Source Maps**: The `source-map` setting helps generate source maps that map the bundled code back to the original source files. This is crucial for debugging in development because it allows you to trace errors and warnings back to the original source code instead of the bundled code.

#### 5. **Module Rules**
```js
module: {
    rules: [
        {  
            test: /\.ts(x?)$/, 
            loader: "ts-loader",
            exclude: /node_modules/
        },
        { 
            enforce: "pre", 
            test: /\.js$/, 
            loader: "source-map-loader" 
        },
        {
            test: /\.css$/,
            exclude: /\.useable\.css$/,
            loader: "style-loader!css-loader"
        },
        {
            test: /\.scss$/,
            loader: 'style-loader!css-loader!sass-loader'
        },
        {
            test: /bootstrap\/js\//,
            loader: 'imports-loader?jQuery=jquery'
        },
        {
            test: /\.html$/,
            loader: 'html-loader'
        }
    ]
}
```
- **TypeScript and JSX/TSX**: The rule `{ test: /\.ts(x?)$/, loader: "ts-loader" }` handles TypeScript and TSX files. It uses the `ts-loader` to transpile TypeScript code into JavaScript.
- **Source Map Loader**: The `source-map-loader` processes JavaScript files before they are bundled to include source maps, which help in debugging.
- **CSS and SCSS**: The `style-loader` and `css-loader` handle CSS files, injecting styles into the page. `sass-loader` is used to process SCSS files.
- **Imports Loader**: The `imports-loader` injects jQuery into specific libraries like Bootstrap that require jQuery as a dependency.
- **HTML Loader**: The `html-loader` handles HTML files, allowing you to import and process them in your JavaScript.

#### 6. **Plugins**
```js
plugins: [
    new HtmlWebpackPlugin({
      template: "src/index.html",
      hash: true
    }),
    new webpack.ProvidePlugin({
        $: 'jquery',
        jQuery: 'jquery',
        'window.jQuery': 'jquery',
        'window.jquery': 'jquery'
    })
]
```
- **HtmlWebpackPlugin**: Automatically generates an HTML file that includes the bundled JavaScript file(s). The `hash: true` option ensures that a unique hash is added to the script tags, forcing the browser to reload the new version whenever the bundle changes.
- **ProvidePlugin**: Automatically loads jQuery when it is referenced in the code, so you don’t need to `import` it in every file where it's needed.

### Summary
This Webpack configuration is designed to build a React app using TypeScript and Redux, with a development server that supports live reloading, proxying API requests, and handling CSS/SCSS. The configuration is well-suited for modern single-page applications and includes various loaders and plugins to handle different asset types, enabling smooth development and debugging.


## In COnfig File
```json
// Copyright (c) Microsoft. All rights reserved.
// Licensed under the MIT license. See LICENSE file in the project root for full license information.
var webpack = require("webpack");
var HtmlWebpackPlugin = require("html-webpack-plugin");
var path = require("path");

module.exports = {
    entry: "./src/index.tsx",
    output: {
        filename: "bundle-dev.js",
        path: path.resolve(__dirname, "..", "public"),
        publicPath: "/"
    },
    resolve: {
        extensions: [".tsx", ".ts", ".js", ".json", ".html"],
        modules: ["node_modules", path.resolve(__dirname, "..", "src")]
    },
    resolveLoader: {
        modules: ["node_modules"]
    },
    devServer: {
        inline: true,
        contentBase: "public/",
        port: 3001,
        proxy: [
            {
                path: "/api/*",
                target: "http://localhost:3001/"
            }
        ],
        historyApiFallback: true
    },
    devtool: "source-map",
    module: {
        rules: [
            {  
                test: /\.ts(x?)$/, 
                loader: "ts-loader",
                exclude: /node_modules/
            },
            { 
                enforce: "pre", 
                test: /\.js$/, 
                loader: "source-map-loader" 
            },
            {
                test: /\.css$/,
                exclude: /\.useable\.css$/,
                loader: "style-loader!css-loader"
            },
            {
                test: /\.useable\.css$/,
                loader: "style-loader/useable!css"
            },
            {
                test: /\.css$/,
                loader: 'style-loader!css-loader'
            },
            {
                test: /\.scss$/,
                loader: 'style-loader!css-loader!sass-loader'
            },
            {
                test: /bootstrap\/js\//,
                loader: 'imports-loader?jQuery=jquery'
            },
            {
                test: /bootstrap-sass[\/\\]assets[\/\\]javascripts[\/\\]/,
                loader: 'imports-loader?jQuery=jquery'
            },
            {
                test: /\.html$/,
                exclude: /node_modules/,
                loader: 'html-loader'
            },
            {
                test: /\.woff(2)?(\?v=[0-9]\.[0-9]\.[0-9])?$/,
                loader: 'url-loader?limit=10000&mimetype=application/font-woff'
            },
            {
                test: /\.(ttf|eot|svg)(\?v=[0-9]\.[0-9]\.[0-9])?$/,
                loader: 'file-loader'
            }
        ]
    },
    plugins: [
        new HtmlWebpackPlugin({
          template: "src/index.html",
          hash: true
        }),
        new webpack.ProvidePlugin({
            $: 'jquery',
            jQuery: 'jquery',
            'window.jQuery': 'jquery',
            'window.jquery': 'jquery'
        })
    ]
};
```

## in Package.json ---> webpack.dev.js is included
```json
{
    "scripts": {
        "start": "webpack-dev-server --open --config configs/webpack.dev.js",
        "build:dev": "webpack --config configs/webpack.dev.js -d",
        "build:prod": "webpack --config configs/webpack.prod.js",
        "test": "jest",
        "test:update-snapshot": "jest --updateSnapshot"
    },
}
```