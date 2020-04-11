### Configurando um projeto React
# Without create-react-app

## Requeriemntos de Sistema

* Ter o Node.js INstalado
* Ter o Yarn instalado (pode utilizar também o NPM, porém precisa trocar `yarn` ou `yarn add` por `npm` ou `npm install` )


## Iniciar um projeto node

Crie uma pasta em qualquer lugar da sua máquina para abrigar todas as configurações e arquivos do seu projeto.

Abra essa pasta em algum terminal de linha de comando 

```  yarn init -y``` 

Esse comando irá criar um arquivo chamado `package.json` onde teremos uma extrutura próxima a essa dentro dele: 

`> ./package.json`
```
  {
    "name": "boilerplate-react-js",
    "version": "1.0.0",
    "description": "A boilerplate for ReactJs wtihout create-react-app ",
    "main": "index.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [
      "[boilerplate",
      "reactjs",
      "reactdom",
      "webpack",
      "babel]"
    ],
    "author": "João Victor Louzada",
    "license": "MIT"
  }
```

## Configurando a extrutura do projeto

Crie duas pastas agora no mesmo diretorio onde o seu arquivo `package.json` está, uma com o nome `src` outra com o nome `public`, é nelas onde iremos ter nossos arquivos de código futuramente, mas calma que logo você vai entender o motivo de duas pastas separadas.

``` $ mkdir src; mkdir public```

## Instalando o React

Agora vamos instalar o React iremos utilizar os gerenciadores de pacotes para pegar e instalar eles dentro do projeto, rodando o seguinte comando:

``` $ yarn add react react-dom ```

Agora podemos ver que ele criou uma pasta `./node_modules` e dentro dela um emaranho de coisas, que no momento não nos é relevante explicar, porém é dentro dela que o Node.Js organiza todas as nossas libs e depências de terceiros que utilizamos no projeto, e deixa elas registradas no nosso `./package.json` para entender quais libs ele precisa controlar em cada versão. Também foi criado o `yarn.lock` (ou `package-lock.json` se estiver usando o NPM) que é nosso arquivo de cache de depencias. Esse arquivo é relevante ser versionado, ao contrário da pasta `./node_modules` então aqui já vamos criar nosso arquivo de `.gitignore` para ignorar esse diretório e não subir ela junto com nosso projeto ocupando um espaço desnecessário. 

Antes de tudo, vamos rodar um `git init` caso você tenha ele instalado para começar a entender e ouvir nossas mudanças no projeto. e depois é só criar nosso arquivo `.gitignore`

``` $ git init; touch .gitignore; ```

Criamos nosso arquivo agora é só colocar dentro dele `node_modules` que ele vai passar a ignorar a pasta e não subir ela. 

Agora é só rodar um `git add . ` para adicionar tudo que temos no diretorio `./` para o nosso versionamento. 

``` $ git add . ```

Show, tudo ok agora, já podemos continuar! 

Ali em cima instalamos o `react` que é nossa lib pincipal, para construir nossa interface e o `react-dom` que é nossa lib que faz a comunicação do React com a nossa DOM no Browser.

E agora temos nosso `package.json` com a seguinte propriedade:

```
  {
    "dependencies": {
      "react": "^16.13.1",
      "react-dom": "^16.13.1"
    }
  }
```

## Configurando Babel e Webpack 

Vamos rodar o comando para instalar as libs que iremos precisar 

``` $ yarn add @babel/core @babel/preset-env @babel/preset-react babel-loader style-loader css-loader file-loader webpack webpack-cli```

Antes de iniciar a configuração, precisamos criar um arquivo `index.html` na nossa pasta `public` onde vamos ter nosso código que o Browser vai ter acesso futuramente, sem o código React.

``` $ touch public/index.html ```

``` $ touch src/index.js ```

Dentro do arquivo HTML criado vamos definir a seguinte estrutura:

  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>React</title>
    </head>
    <body>
      <div id="app"></div>
      <script src="bundle.js"></script>
    </body>
  </html>

Vamos criar também um aruqivo para configurar o Babel, porém esse precisa ficar na nossa pasta raiz.

``` $ touch babel.config.js ```

E definir a seguinte estrutura para ele:

```
  module.exports = {
    presets: [
      '@babel/preset-env',
      '@babel/preset-react'
    ]
  }
```

Os `presets` exportados pelo babel são configurações que terceiros desenvolveram para ajudar no funcionamento, ou seja, as libs que importamos la em cima, a primeira serve par aque o Babel possa entender em qual ambiente estamos rodando a nossa aplicação e com isso converter par aquele ambiente as funcionalidades que ele ainda não entende (Isso vale para o browser que irá rodar a aplicação como Chrome, Firefox, IE ou outros, e também para o Node.Js que roda o JavaScript do lado do servidor). 

Já a segunda exportação é responsavel por passar para o babel, as funcionaldiades que o React cria, com isso, permitir incluir HTML, CSS, Imagens e outras coisas dentro do nosso código JavaScript.

Agora vamos configurar o webpack, pois ele também tem um arquivo de configuração.

``` $ touch webpack.config.js ```

E dentro dele, agora vamos colocar a seguinte configuração:

```
  const path = require('path')

  module.exports = {
    entry: path.resolve(__dirname, 'src', 'index.js'),
    output: {
      path: path.resolve(__dirname, 'public'),
      filename: 'bundle.js'
    },
    devServer: {
      contentBase: path.resolve(__dirname, 'public)
    }
    module: {
      rules: [
        {
          test: /\.js$/,
          exclude: /node_modules/,
          use: {
            loader: 'babel-loader'
          }        
        },
        {
          test: /\.css$/,
          exclude: /node_modules/,
          use : [
            { loader: 'style-loader'},
            { loader: 'css-loader'},
          ]
        },
        {
          test: /.*\.(gif|png|jpe?g|svg)$/i,
          use: {
            loader: 'file-loader'
          }
        }
      ]
    }
  }
```

Na configuração, inicialmente importamos a lib 'path' que vem do Node.js que é quem executa o webpack no momento que criamos o bundle da aplicacão, ela é usada para definir os caminhos e não gerar erros caso precisemos rodar ela dentro do Windows por exemplo que utiliza a `\` no lugar da `/`, que é comum nos sistemas Unix ( MacOc e Linux ).

Logo depois inicamos a configuração de fato do webpack, o primeiro atributo `entry` é o nosso arquivo de entrada da aplição, ou seja, qual iremos precisar carregar primeiro, que no caso é nosso `./src/index.js`, porém utilizando o path ele fica nessa sintaxe. 

Já o `output` é o arquivo que será gerado após o processo de build do bundle, então passamos o caminho `./public/` com o nome do arquivo em `filename` que é `bundle.js`.

O `module` é para criar modulos de uso dentro do weback, e com ele criamos uma regra para o build, que é verificar os arquivos que finalizam com o nome `.js` (utilizando uma expressão regular), excluindo os arquivos que estão na pasta `node_modules` e usando o `babel-loader`. 

A segunda regra é para tratar arquivos CSS, sendo o primeiro loader para injetar o CSS dentro do nosso HTML e o segundo loader é para entender sobre os arquivos CSS dentro do JavaScript quando forem importados.

Por fim a ultima regra é para tratar importação de imagens por parte do nosso JavaScript, ele utiliza o file-loader para importar imagens `gif; png; jpg/jpeg e svg`.

Podemos testar se está tudo ok usando o comando: 

``` $ yarn webpack --mode development ``` 

E ao executar ele deve criar um arquivo `bundle.js` na nossa pasta public usando nosso arquivo `index.js` dentro da pasta `src` para leitura.

Tudo certo ? Ainda não, ainda precisamos configurar agora o ambiente de desenvolvimento, pois ainda temos o live-reload sem configurar. Vamos instalar nosso servidor de desenvolvimento do webpack, o webpack-dev-server

```yarn add webpack-dev-server -D```

Passamos o `-D` no final pois essa funcionalidade só precisa ser utilizada no ambiente de desenvolvimento. 

Ele ja ficou configurado no nosso `webpack.config.js` com o `devServer`

Para iniciar o servidor em desenvolvimento, podemos rodar: 

``` $ yarn webpack-dev-server --mode development```

Falta agora a configuração de fato do react para poder iniciar nossos trabalhos com React, para isso iremos criar um outro arquivo que é nosso primeiro componente, e o pai de todos que irão ser criados depois, é ele quem irá chamar toda nossa aplicação a ser carregada.

``` $ touch src/App.js ```

Note que criei o arquivo com uma letra `A` no inicio em maiúsculo, pois, todo componenten no React inicia com a letra maiuscula. 

Dentro dele iremos escrever já com a sintaxe do React nosso primeiro componente teste, que é:

```
  import React from 'react';

  export default function App() {
    return (
        <h1>Hello React</h1>
    );
  }
```

Note que nela importamos o React e depois exportamos uma função `App` que retorna um H1 com um texto dentro, porém em nenhum momento usamos a função React no código. Isso ocorre pois o React precisa estar importado mesmo que não seja usado visivelmente pois temos código JSX(ou HTML) dentro do nosso arquivo `.js` e se não tivermos nosso React importado, o arquivo não irá rodar pois não consiguira entender o código JSX retornado da função. 

Agora vamos no nosso arquivo de entrada da aplicação que configuramos no webpack, nosso `index.js` dentro da pasta `src` e colocamos o seguinte código: 

``` 
  import React from 'react'
  import {render} from 'react-dom'

  import App from './App'

  render(<App />, document.getElementById('app'))
```

Ali mais uma vez importamos o React e agora também o método render, de dentro do react-dom, que é para permitir a renderização do React na nossa DOM do navegador.
Também importamos nosso arquivo `App.js` que exporta por default um componente `App` e passamos ele com a declarativa de um componente dentro do método `render()`para ser renderizado dento de um elemento com o id 'app' no nosso HTML. Ele vai procurar la no `./public/index.html` a div que definimos anteriormente, e todo nosso código react gerado de agora para frente, todo mesmo, cada parte, será inserido dentro dessa mesma div. 

Para facilitar o nosso servidor, para automatizar vamos no nosso `package.json` e criar um script de incialização. 

```
  "scripts": {
    "start": "webpack-dev-server --mode development",
    "build": "webpack --mode production"
  },
```
Fomos até os nossos scripts e removemos os scripts de tests que não estavam sendo utilizados e inserimos um script novo chamado start, que executa o comando para iniciar nosso servidor de desenvolviemnto, agora é só rodar `yarn start` que tudo irá rodar facilmente. 

O segundo script, chamado `build` é para criar um build da aplicação para ser enviado para produção ao final do processo de desenvolvimento das nossas futuras features. 