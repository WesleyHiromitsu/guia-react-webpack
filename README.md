# Criar um projeto react do zero com Webpack

Guia para ajudar a construir um projeto react do zero com Webpack, de forma rápida e resumida, utilizando yarn.

## Criar pasta do projeto

```bash
mkdir project-name
cd project-name
```

## Inicie seu projeto.

```bash
yarn init -y
```

## Instalação dos pacotes.

```bash
yarn add react react-dom
```

## instalação dos pacotes de desenvolvimento.

```bash
yarn add -D @babel/core @babel/preset-env @babel/preset-react autoprefixer babel-loader css-loader file-loader html-webpack-plugin postcss-loader style-loader url-loader webpack webpack-cli webpack-dev-server
```

## Adicione scripts em package.json

```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "webpack-dev-server --open --hot --mode development",
    "build": "webpack --mode production"
  }
```

## Adicione as seguintes pastas e arquivos no projeto.

Crie uma pasta public e coloque um arquivo index.html.

> Você pode optar por digitar esse comando para criar a pasta e o arquivo.

```bash
mkdir public
touch public/index.html
```

Crie uma pasta src e coloque coloque os arquivos index.js e App.js.

> Você pode optar por digitar esse comando para criar a pasta e o arquivo.

```bash
mkdir src
touch src/index.js src/App.js
```

## Adicione o seguinte código no arquivo que acabamos de criar.

Abra o arquivo index.html da pasta public e adicione o código:

```
<!DOCTYPE html>
<html lang="pt">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>My React App</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

Agora abra o arquivo App.js da pasta src e adicione o código:

```
import React from 'react';

function App() {
  return <h1>Deu certo!</h1>;
}

export default App;
```

E por fim adicione o seguinte código no arquivo index.js da pasta src:

```
import React from "react";
import ReactDOM from "react-dom";

import App from './App';

ReactDOM.render(
  <App />,
document.querySelector("#root"));
```

## Crie o arquivo .babelrc na raiz do projeto.

Crie um arquivo .babelrc na raiz do projeto.

> Você pode optar por digitar esse comando para criar o arquivo.

```bash
touch .babelrc
```

Abra o arquivo e adicione o seguinte código.

```
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

## Crie o arquivo webpack.config.js na raiz do projeto.

Crie um arquivo webpack.config.js na raiz do projeto.

> Você pode optar por digitar esse comando para criar o arquivo.

```bash
touch webpack.config.js
```

Abra o arquivo e adicione o seguinte código.

```
const path = require('path');
const autoprefixer = require('autoprefixer');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    entry: './src/index.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js',
        chunkFilename: '[id].js',
        publicPath: ''
    },
    resolve: {
        extensions: ['.js', '.jsx']
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                loader: 'babel-loader',
                exclude: /node_modules/
            },
            {
                test: /\.css$/,
                exclude: /node_modules/,
                use: [
                    { loader: 'style-loader' },
                    {
                        loader: 'css-loader',
                        options: {
                            modules: {
                                localIdentName: "[name]__[local]___[hash:base64:5]",
                            },
                            sourceMap: true
                        }
                     },
                     {
                         loader: 'postcss-loader',
                         options: {
                             ident: 'postcss',
                             plugins: () => [
                                 autoprefixer({})
                             ]
                         }
                      }
                ]
            },
            {
                test: /\.(png|jpe?g|gif)$/,
                loader: 'url-loader?limit=10000&name=img/[name].[ext]'
            }
        ]
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: __dirname + '/public/index.html',
            filename: 'index.html',
            inject: 'body'
        })
    ]
};
```

## Estrutura das pastas

No final a estrutura de pastas do seu projeto deverá ficar assim:

    ├── public
    │   └──index.html
    ├── src
    │   ├── App.js
    │   └── index.js
    ├── .babelrc
    ├── package.json
    ├── webpack.config.js
    └── yarn.lock

## Inicie o projeto

```bash
yarn start
```
