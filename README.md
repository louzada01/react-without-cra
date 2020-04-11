## O que é o REACT ? 

Uma tec para construir interfaces
Ele pode construir qualquer interface 
Ele trabalha com SPA - Single Page Application 
SPA é um conceito, não tecnologia 
Antes do SPA o Back-end ele devolvia em cada rota um HTML, agora com o spa ele devolve uma unica pagina e dentro dela ele cuida no front-end esse roteamento, apenas mudando o conteudo
Isso permite performance, usabilidade e UX 
React por si só é uma LIB, mas o ecossistema é um Framework
Tudo fica dentro do JS, tudo é JS, tudo é devolvido JS
React a LIB, ReactJS (REACT + REACT DOM) é o Framework Web, ReatNative é o Framework Mobile


## Quais as vantagens do React ? 

- Organização do código 

Componentização - Tudo é um novo componente, separando os itens
Ele cria um componente Pai para todos os outros e dentro deles temos filhos e netos (...) 

- Divisão de Responsabilidades

Back-End cuida da regra de negocios enquanto o front-end cuida da interface e de toda a interação com o usuário, com isso o usuario tem menos contato com a regra de negocios em si compartilhada

Estrutura com multiplos clients com uma API de acesso (JSON) permitindo assim uma estrutura como um Client, Back-Office, Mobile e Partners. 

- Programação declarativa

## JSX 

Permite escrever HTML dentro do JavaScript

Com o react podemos criar nossos proprios componentes e elementos ( alem de usar os elemntos ja criados no HTML como button, div, section e etc...)

## Programação Imperativa vs Declarativa

# Imperativa 

Falar o que o computador precisa fazer

# Declarativa 

Falar o que você quer que o computador te responda

## Babel e Webpack - O que é  ?

O Browser não entende nosso código escrito em JS, por isso, precisamos utilizar essas ferramentas para traduzir o código e ajudar o Browser para interpretar.

# Babel 

- Permite que o código escrito em JS ( normalmnet ES6++ ) para código JS Vanilla, permitindo assim que o navegador entenda de fato o que está sendo escrito em uma sintaxe mais atualizada. 

# Webpack

- Cria um bundle com todo o código JS escrito, em um unico arquivo com todos os scripts

- Ele é quem permite o Babel entender e transmutar o código para o Browser, mostra o JS como importar os arquivos (CSS, Imagens e etc)

- Permite live-reload com o Webpack Dev Server, o que faz com que ao salvar as modificações no código a página já seja atualizada e mostre as modificações em tela para o desenvolvedor



