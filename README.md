<h1 align="center"><a href="https://pt-br.reactjs.org/" target="_blank" style="text-decoration: none">
    <img alt="ReactJs" src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9Ii0xMS41IC0xMC4yMzE3NCAyMyAyMC40NjM0OCI+CiAgPHRpdGxlPlJlYWN0IExvZ288L3RpdGxlPgogIDxjaXJjbGUgY3g9IjAiIGN5PSIwIiByPSIyLjA1IiBmaWxsPSIjNjFkYWZiIi8+CiAgPGcgc3Ryb2tlPSIjNjFkYWZiIiBzdHJva2Utd2lkdGg9IjEiIGZpbGw9Im5vbmUiPgogICAgPGVsbGlwc2Ugcng9IjExIiByeT0iNC4yIi8+CiAgICA8ZWxsaXBzZSByeD0iMTEiIHJ5PSI0LjIiIHRyYW5zZm9ybT0icm90YXRlKDYwKSIvPgogICAgPGVsbGlwc2Ugcng9IjExIiByeT0iNC4yIiB0cmFuc2Zvcm09InJvdGF0ZSgxMjApIi8+CiAgPC9nPgo8L3N2Zz4K" width="50%"/>
    <br>
    Introdução ao ReactJs
</a></h1>

## Descrição

Este projeto está sendo desenvolvido em <strong>[ReactJs](https://pt-br.reactjs.org/)</strong> para fins de capacitação pessoal

## Etapas

- Antes de iniciar o projeto ReactJs, é necessário definir em qual diretório o projeto irá ficar armazendo e executar o comando para criar o arquivo <strong>package.json</strong>, o qual irá conter informações sobre o projeto e bibliotecas adicionadas:

```js
yarn init -y
```

- Para criar um projeto React é necessário instalar o <strong>React</strong> e o <strong>React-Dom</strong>. O React é o framework do react e o React-Dom é bibblioteca para desenvolvimento para web:

```js
yarn add react react-dom
```

- No diretório do projeto, criar as pastas <strong>public</strong> e <strong>src</strong>;

- Para que os navegadores web consigam interpretar os códigos javascript nas páginas HTML é necessário configurar o <strong>Babel</strong>, para converter (transpilar) o código do React pera um código que o browser entenda;

- Junto com o <strong>Babel</strong> é necessário configurar o <strong>Webpack</strong>, para cada tipo de arquivo (.js, .css, .png) vai converter o código de uma maneira diferente;

- Para realizar essas configurações, é necessário intalar o <strong>@babel/core</strong> <string>@babel/preset-env</strong>: converte um código js mais moderno para um código js mais antigo, mas baseado no ambiente da aplicação. <strong>@babel/preset-react</strong>: adiciona as funcionalidades do react na conversão. <strong>webpack</strong> <strong>webpack-cli</strong>:

```js
yarn add @babel/core @babel/preset-env @babel/preset-react webpack webpack-cli
```

- Após a instalação vamos criar o arquivo <strong>babel.config.js</strong> na raiz do projeto, o qual irá conter as configurações do babel, a maneira que o código js é convertigo para código que o browser compreenda;

```js
module.exports = {
  presets: ["@babel/preset-env", "@babel/preset-react"],
};
```

- Para verificar se a configuração está correta, vamos criar um arquivo <strong>index.js</strong> no diretório <i>src</i>, com uma <strong>arrow function</strong>:

```js
const soma = (a, b) => {
  return a + b;
};

console.log(soma(1, 3));
```

- Para testar a funcionalidade configurada, vamos instalar o <strong>@babel/cli</strong>, que permite rodar o projeto via linha de comando, em seguida utilizar a funcionanlida adicionada para adicionar o código em outro arquivo, no caso <strong>bundle.js</strong>:

```js
yarn add @babel/cli
yarn babel src/index.js --out-file public/bundle.js
```

- Com o código convertido, podemos adicionar o arquivo convertido, <strong>bundle.js</strong>, no arquivo index.html:

```js
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>ReactJS</title>
  </head>
  <body>
    <div id="app"></div>

    <script src="bundle.js"></script>
  </body>
</html>
```

- Para configurar o <strong>webpack</strong>, vamos criar o arquivo <i>webpack.config.js</i> na raiz do projeto, ele vai automatizar o processo de identificar o tipo de arquivo que está sendo requisitado na aplicação

```js
const path = require("path");

module.exports = {
  entry: path.resolve(__dirname, "src", "index.js"),
  output: {
    path: path.resolve(__dirname, "public"),
    filename: "bundle.js",
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
        },
      },
    ],
  },
};
```

- Instalar o <strong>babel-loader</strong> que será o loader do babel:

```js
yarn add babel-loader
```

- Para converter o projeto:

```js
yarn webpack --mode development
```

- Instalar o <strong>webpack-dev-server</strong> em modo de desenvolvedor, -D, ele é o servidor de desenvolvimento do webpack;

```js
yarn add webpack-dev-server -D
```

- Para rodar o projeto com o webpack server:

```js
yarn webpack serve --mode development
```

- Componentização: dividir pedaços da aplicação em componentes, divir em pequenas partes que poderão ser reaproveitado em várias outras partes do projeto.

- Componente <i>render</i> do <u>react-dom</u>: utilizado para renderizar elementos do js no html.

```js
import React from "react";
import { render } from "react-dom";

render(<h1>Hello World</h1>, document.getElementById("app"));
```

- Componentes no ReactJs sempre deverão ser declaradas com a primeira letra em maiúscula, devem possuir o React importado, uma função com o nome do componente e o exportar com o <strong>export default</strong>.

```js
import React from "react";

function App() {
  return <h1>Hello World</h1>;
}

export default App;
```

- Para utilizar o componente criado, basta importar o componente no arquivo que deseja utilizar e declarar como uma tag html:

```js
import React from "react";
import { render } from "react-dom";

import App from "./App";

render(<App />, document.getElementById("app"));
```

- Para utilizar mais de um componente na mesma <strong>function</strong>, basta declarar dentro de uma <i>div</i>:

```js
import React from "react";

import Header from "./components/Header";

function App() {
  return (
    <div>
      <h1>Hello World!</h1>
      <Header />
    </div>
  );
}

export default App;
```

- Fragment: utilizado para criar um container, porém sem reproduzir conteúdo na dom, como uma nova tag html:

```js
<>
  <h1>Hello World!</h1>
  <Header />
</>
```

- Propriedade: alguma informação que pode ser passada de um componente pai para um componente filho.

```js
PAI
<>
  <h1>Hello World!</h1>
  <Header title="Homepage" />
  <Header />
</>

FILHO
export default function Header(props) {
  return (
    <header>
      <h1>{props.title}</h1>
    </header>
  );
}
```

- As propriedades podem ser desetruturadas, informando somente o conteúdo que será utilizado, sem a necessidade de passar a propriedade toda:

```js
export default function Header({ title }) {
  return (
    <header>
      <h1>{title}</h1>
    </header>
  );
}
```

- As propriedades podem receber conteúdos html, as quais são chamadas de children:

```js
<>
  <h1>Hello World!</h1>
  <Header title="Homepage" />
  <Header>
    <ul>
      <li>Home</li>
      <li>Projects</li>
      <li>Login</li>
    </ul>
  </Header>
</>
```

- Para acessar o conteúdo gerado, basta declarar o children no parâmetro da função e declarar no local que deseja ser mostrado em tela:

```js
export default function Header({ title, children }) {
  return (
    <header>
      <h1>{title}</h1>
      {children}
    </header>
  );
}
```

- Estado: possibilidade de alterar o estado das informações mostradas em tela, podendo ser adicionado, removido ou atualizado o aconteúdo e mostrado em tempo real. Para utilizar o conceito de estado, é necessário utilizar o <strong>useState</strong>, ela retorna um array com duas posições, sendo a primeira a variável com seu valor inicial e a segunda posição a função para atualizar o valor.
- Imutabilidade: não é possível alterar uma variável, apenas recriar a variável com as novas informações, para isso utilizamos o <strong>spread operator</strong> para copiar o conteúdo da variável e em seguida adicionar o novo conteúdo.

```js
import React, { useState } from "react";

import Header from "./components/Header";

function App() {
  const [projects, setProjects] = useState([
    "Desenvolvimento de App",
    "Front-end web",
  ]);

  function handleAddProject() {
    setProjects([...projects, `Novo projeto ${Date.now()}`]);
  }

  return (
    <>
      <Header title="Projects" />
      <ul>
        {projects.map((project) => (
          <li key={project}>{project}</li>
        ))}
      </ul>

      <button type="button" onClick={handleAddProject}>
        Adicionar projeto
      </button>
    </>
  );
}

export default App;
```

- map(): percorre algum conteúdo retornando alguma coisa desse conteúdo.

- Para estilizar o projeto, vamos utilizar o <strong>style-loader</strong> e o <strong>css-loader</strong>:

```js
yarn add style-loader css-loader
```

- Configurar o <i>webpack.config.js</i> para ler e interpretar os arquivos de css e injetar o css no html:

```js
{
  test: /\.css$/,
  exclude: /node_modules/,
  use: [{ loader: "style-loader" }, { loader: "css-loader" }],
},
```

- Podemos configurar um arquivo de estilização css:

```css
* {
  margin: 0;
  padding: 0;
  outline: 0;
  box-sizing: border-box;
}

body {
  background: #f5f5f5;
  font: 14px sans-serif;
  color: #333;
}
```

- Importar o aquivo css para o projeto:

```js
import "./App.css";
```

- Instalar o <strong>file-loader</strong>, que vai ser utilizado para carregar arquivos na aplicação:

```js
yarn add file-loader
```

- Configurar o webpack com o file-loader:

```js
{
  test: /.*\.(gif|png|jpe?g)$/i,
  use: {
    loader: "file-loader",
  },
},
```

- Importar uma imagem para o projeto e adicionar no local desejado:

```js
import backgroundImage from "./assets/background.jpeg";

<img width={300} src={backgroundImage} />;
```

## Tecnologias

- [nodeJS](https://nodejs.org/)
- [yarn](https://yarnpkg.com/)
- [express](https://github.com/expressjs/express)
- [nodemon](https://github.com/remy/nodemon)
- [uuidv4](https://github.com/thenativeweb/uuidv4)

---

Desenvolvido por [Johnatan Luiz Osterloh](https://www.linkedin.com/in/johnatanosterloh/)

```

```
