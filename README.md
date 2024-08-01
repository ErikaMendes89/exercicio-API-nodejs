<h1>Exercicio de API com Middleware ✍🏾📚</h1>
<br>
<p>Este é um exercício desenvolvido com base no curso da Microsoft Learn sobre APIs e middleware utilizando Node.js e Express.<br>
O exercício consiste em duas partes principais: o servidor (app.js) e o cliente (client.js).</p>

## Descrição

Este projeto demonstra o uso de middleware em uma API criada com Node.js e Express.
O middleware é uma função que é executada durante o ciclo de vida de uma requisição HTTP, permitindo a implementação de lógica adicional antes que a requisição chegue ao manipulador de rota final.

## Arquivos Envolvidos
<ol>
  <li><b>app.js:</b> Este arquivo contém o servidor Express que define algumas rotas e utiliza um middleware para verificar a autorização.</li>
  <li><b>client.js:</b> Este arquivo contém um cliente HTTP simples que faz uma requisição à rota protegida do servidor.</li>
</ol>

## Estrutura do Projeto

<b>app.js</b>

* Importa o módulo `express` e cria uma instância da aplicação.</li>
* Define um middleware chamado `isAuthorized` que verifica se o cabeçalho de autorização está presente e se é válido.</li>
* `/users` : Rota protegida pelo middleware `isAuthorized`que retorna uma lista de usuários.</li>
* `/products` : Rota que retorna uma lista de produtos.
* O servidor é configurado para escutar na porta 3000.<br>

  *O CODIGO:*

~~~javascript
const express = require("express");
const app = express();

function isAuthorized(req, res, next) {
  const authHeader = req.headers.authorization;
  
  if (!authHeader || authHeader !== 'secretpassword') {
    return res.status(401).send('unauthorized: Access Denied');
  }

  next();
}

const port = 3000;

app.get("/", (req, res) => res.send("Hello World!"));

app.get("/users", isAuthorized, (req, res) => {
  res.json([
    {
      id: 1,
      name: "User Userson",
    },
  ]);
});

app.get("/products", (req, res) => {
  res.json([
    {
      id: 1,
      name: "The Bluest Eye",
    },
  ]);
});

app.listen(port, () => console.log(`Example app listening at http://localhost:${port}`));

~~~
<br><br>
## 

**client.js**

* Importa o módulo http e define as opções de requisição, incluindo o cabeçalho de autorização.
* Faz uma requisição GET à rota /users do servidor.
* Imprime o status da conexão, os dados recebidos e mensagens de fim de conexão e erro.

~~~ javascript
const http = require('http');

const options = {
  port: 3000,
  hostname: 'localhost',
  path: '/users',
  headers: {
    authorization: 'secretpassword'
  },
};

const req = http.get(options, (res) => {
  console.log(`Connected - Status Code ${res.statusCode}`);

  res.on('data', (chunk) => {
    console.log("Chunk data: ", chunk.toString());
  });

  res.on('end', () => {
    console.log('No more data');
  });

  res.on('close', () => {
    console.log('Connection closed');
  });
});

req.on('error', (error) => {
  console.error('An error occurred: ', error);
});

req.end();

~~~

# Executando o Projeto:
## Para executar este projeto, siga as instruções abaixo:

* Certifique-se de ter o Node.js instalado.
* Clone este repositório.
* Navegue até o diretório do projeto.
* Execute node `app.js` para iniciar o servidor.
* Em outro terminal, execute node `client.js` para iniciar o cliente e fazer a requisição à rota protegida.

## Conclusão
Este exercício demonstra como usar middleware para implementar autenticação simples em uma API criada com Node.js e Express, além de como criar um cliente HTTP para interagir com esta API.
Os arquivos encontram-se no caminho node-essentials\nodejs-http\exercise-express-middleware




