# treinamento-api
Aplicações web  com API Rest Java Script e Front End Vue.Js

## ✨ Introdução
Olá, esta documentação tem como objetivo auxiliar quem está iniciando estudos para desenvolvimento web com Java Script, node e demais ferramentas que compões o enorme lista de ferramentas que podem ser utilizadas.

Inicialmente é importante ressaltar que no modelo que será abordado é composto por 2 aplicações: a primeira conhecida como backend ou API é responsável pela manipulação das informações, gravação na base de dados e compõe toda ou boa parte da regra de negócio da aplicação; a segunda também conhecida como front end é a aplicação que contem as telas ou seja, a interface com o usuário. Essa mesma se comunica com a API através de requisições ou chamadas HTTP para obter ou enviar dados para serem salvos na base de dados.

Alguns exemplos de requisições podem ser acessadas nesse link.

Requisitos para desenvolvimento da API:
- [NodeJs](https://nodejs.org/en/)
- [Yarn](https://yarnpkg.com/)
- [Postman](https://www.postman.com/)
- [MariaDB](https://mariadb.org/)
- [VSCode](https://code.visualstudio.com/)

OBS: Existem diversos materiais na internet explicando como instalar cada uma das ferramentas citadas. Logo nesse tutorial não será explicado o processo de instalação dos mesmos.

Criando a API
É recomendado criar uma pasta para o projeto. Sendo assim criaremos uma pasta chamada treinamento e dentro dela seguiremos os demais passos:


mkdir treinamento
cd treinamento
Criaremos um diretório para iniciarmos nossa aplicação:


mkdir api
cd api
Certo de ter o Node instalado na computador que estiver utilizando, execute o comando para iniciar o repositório:


npm init -y
Pronto com o repositório iniciado um arquivo chamado package.json será criado. Ele é o responsável por conter scripts para iniciar ou compilar a aplicação e também controla os pacotes de dependências do projeto com suas versões.

Estrutura de pastas do projeto
O exemplo demonstrado possui a seguinte estrutura de pastas:

```
/src
  /auth
  /config
  /controller
  /router
index.js
package.json
.env
```

Onde:
```
  /src é a pasta raiz que contem todo o código fonte macro.
  /src/auth é a pasta que contem os controles de acesso como login e verificação de token.
  /src/config é a pasta reservada para conter arquivos de configuração como a configuração de acesso ao banco de dados por exemplo.
  /src/controller é a pasta que conterá os arquivos com as funções de crud do nosso projeto
  /src/router local onde criaremos os arquivos de configuração de rotas.
```
OBS: A estrutura de pastas deverá ser criada manualmente. Inclusive os arquivos index.js e .env.

Ao final do projeto teremos uma pasta como na imagem:


Arquivo principal do projeto index.js
O Arquivo index.js na raiz do projeto ao lado de package.json é o ponto de partida para a nossa aplicação. Ele é o responsável por carregar todos os arquivos do projeto e servi-lo em uma porta para ser acessado por requisições.

o Conteúdo do index.js deve ser:

```
  // Importação de pacotes
  require('dotenv').config()
  const express = require('express')
  const cors = require('cors')
  const bodyParser = require('body-parser')
  const consign = require('consign')
  const knex = require('knex')
  const config = require('./src/config/db')

  // instanciação da varíavel global app
  const app  = express()

  app.use(cors())
  app.use(bodyParser.json())

  // Carregamento da configuração do banco de dados
  const database = knex(config)
  app.db = database

  // Carregamento dos arquivos para a variavel global app.
  consign()
  .include('./src/controller')
  .include('./src/auth')
  .include('./src/router')
  .into(app)

  // Inicialização do serviço
  app.listen(process.env.APP_PORT, () => {
    console.log(`Rodando na porta ${process.env.APP_PORT}`)
  })
```

Podemos ver que logo no inicio tem a declaração de diversas variáveis recebendo como valor a importação de algum pacote. A importação se dá da seguinte forma:  A lista de todos os pacotes que serão utilizados no exemplo está na tag "dependencies": {} do arquivo package.json abaixo.


const variavelTeste = require('nome-pacote');
Controlador de dependências package.json
Substitua o arquivo package.json pelo seguinte: 


{
  "name": "api",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "nodemon"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "body-parser": "^1.19.0",
    "consign": "^0.1.6",
    "cors": "^2.8.5",
    "dotenv": "^10.0.0",
    "express": "^4.17.1",
    "jsonwebtoken": "^8.5.1",
    "knex": "^0.95.14",
    "mysql": "^2.18.1",
    "nodemon": "^2.0.15",
    "validate.js": "^0.13.1"
  }
}
Lista de dependências da API
Para instalarmos um pacote manualmente, podemos utilizar os seguintes comandos:


yarn add express
ou


npm i --save express
Explicação da finalidade de alguns dos pacotes citados:

body-parser -> quando enviamos uma requisição com dados no body, o servidor precisa pegar esses dados em forma de objetos. Para isso esse pacote transforma o data do request em Object.

consign -> esse pacote é responsável por ler todos os arquivos dentro de /src e injeta-los dentro da variável global app. Assim todas as funções podem ser acessadas de outros arquivos apenas chamando “app.arquivo.funcao-do-arquivo“

dotenv -> Responsável por ler o arquivo oculto ".env" presente na raiz do projeto.

express → pacote responsável por servir rotas em uma porta em forma de serviço HTTP

jsonwebtoken -> pacote responsável por gerar uma token com dados do usuário contendo um prazo de validação para uso. O mesmo também consegue validar se a token está expirada ou nao.

knex -> Responsável por realizar a conexão com o banco de dados de forma amigavel, também conhecido como queryBuilder.

mysql -> Lib utilizada pelo knex para se conectar ao banco mysql ou mariadb.

nodemon -> Monitora sempre que alteramos um arquivo e faz um reload automatico no projeto.

validate.js -> Responsável por comparar um objeto com uma validação de preenchimento e tipagem de dados afim de verificar se as informações enviadas na requisição estão corretas.














Lista de pacotes:

npm: body-parser 
https://www.npmjs.com/package/body-parser

npm: consign 
https://www.npmjs.com/package/consign

npm: cors 
https://www.npmjs.com/package/cors

npm: dotenv 
https://www.npmjs.com/package/dotenv

Express - framework de aplicativo da web Node.js 
https://expressjs.com/pt-br/

npm: jsonwebtoken 
https://www.npmjs.com/package/jsonwebtoken

Knex.js - A SQL Query Builder for Javascript 
https://knexjs.org/

npm: mysql 
https://www.npmjs.com/package/mysql

npm: nodemon 
https://www.npmjs.com/package/nodemon

validate.js 
https://validatejs.org/
 
 
<h1 align="center">Implementação do controller</h1>
Na pasta /src/controller criar um arquivo chamado produto.js uma vez que será desenvolvido um cadastro de produto como exemplo:

// Importamos o pacote validate.js para validar campos obrigatórios de preenchimento
const validate = require('validate.js')

// exportamos o módulo recebendo como parâmetro a variavel global app
module.exports = app => {

// variavel com a validação de campos obrigatórios para salvar
  const validateSalvar = {
    descricao: { presence: true, type: 'string' },
    quantidade: { presence: true, type: 'number' },
    valor: { presence: true, type: 'number' }
  }

// variavel com a validação de campos obrigatórios para editar
  const validateEditar = {
    id: { presence: true, type: 'integer' },
    ...validateSalvar
  }

  // Função listar é asincrona e recebe request e retorna uma responsse
  const listar = async (req, res) => {
    try {
      // Constante que obtem a lista de produtos no banco
      // app.db é a variavel de conexao com o banco de dados configurado no index.js
      const resp = await app.db('produto').select()

      // retornoda função listar retorna a variavel resp com a lista de produtos do banco de dados
      return res.json(resp)
    } catch (error) {
      // caso ocorrer algum erro, uma menssagem de erro será retornada
      return res.json({ erro: error.message })
    }
  }

  // Função exibir é assincrona e recebe a requisição e retorna uma resposta
  const exibir = async (req, res) => {
    try {
      // A diferença é que nesse caso deve retornar um produto caso o id seja correspondente ao informado na requisição.
      const resp = await app.db('produto')
      .where({
        id: req.params.id
      })
      .select()

      // Retorna o primeiro resultado encontrado.
      return res.json(resp[0])
    } catch (error) {
      // Caso ocorra alguma falha, retorna um erro
      return res.json({ erro: error.message })
    }
  }

  // Função editar
  const editar = async (req, res) => {
    try {
      // Valida com a variavel validate se todos os campos obrigatórios foram passados no req.body
      const err = validate(req.body, validateEditar)
      // Caso não retorna uma menssagem de erro
      if (err) return res.json(err)

      // Ao tentar editar um produto. Verifica se o mesmo existe na base de dados
      const findOne = await app.db('produto')
      .where({
        id: req.body.id
      })
      if (!findOne.length) throw new Error('Produto não encontrado')

      // Caso exista então aplica um update para atualizar as informações
      await app.db('produto')
        .where({
          id: req.body.id
        })
        .update({
          descricao: req.body.descricao,
          quantidade: req.body.quantidade,
          valor: req.body.valor
        })

      return res.json({ message: 'Alterado' })
    } catch (error) {
      return res.json({ erro: error.message })
    }
  }

  const salvar = async (req, res) => {
    try {
      const err = validate(req.body, validateSalvar)
      if (err) return res.json(err)
      
      await app.db('produto')
        .insert({
          descricao: req.body.descricao,
          quantidade: req.body.quantidade,
          valor: req.body.valor
        })
  
      return res.json({ message: 'Inserido' })
    } catch (error) {
      return res.json({ erro: error.message })
    }
  }

  const deletar = async (req, res) => {
    try {
      const findOne = await app.db('produto')
        .where({
          id: req.body.id
        })
        if (!findOne.length) throw new Error('Produto não encontrado')

      await app.db('produto')
        .where({
          id: req.params.id
        })
        .del()

      return res.json({ message: 'Deletado' })

    } catch (error) {
      return res.json({ erro: error.message })
    }
  }

  // Para ser acessadas de outros arquivos todas as funçoes devem ser exportadas.
  return {
    listar,
    exibir,
    editar,
    salvar,
    deletar
  }
}




<p align="center">
  <a href="#-tecnologias">Tecnologias</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-como-executar">Como executar</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#-licença">Licença</a>
</p>

<p align="center">
  <img alt="License" src="https://img.shields.io/static/v1?label=license&message=MIT&color=8257E5&labelColor=000000">
  <img src="https://img.shields.io/static/v1?label=NLW&message=Heat&color=8257E5&labelColor=000000" alt="NLW Heat" />
</p>


## 🚀 Como executar

> Obs.: Nesse projeto temos autenticação via OAuth com o GitHub

- Clone o repositório e acesse a pasta;
- Faça uma copia do arquivo `.env.example` para `.env` e preencha com as suas credenciais do GitHub;
- Instale as dependências com `yarn`;
- Executa as migrations com `yarn prisma migrate dev`;
- Inicie o servidor com `yarn dev`;

A aplicação pode ser acessada em [`localhost:4000`](http://localhost:4000).

## 📄 Licença

Esse projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

Feito com ♥ by Rocketseat 👋🏻 &nbsp;[Participe da nossa comunidade!](https://discordapp.com/invite/gCRAFhc)


## 🔗 Links uteis

Documentacao: https://eder-ferraz-caciano.atlassian.net/wiki/spaces/~775927082/blog/2021/12/29/33020/Aplica+es+web+com+API+Rest+Java+Script+e+Front+End+Vue.Js

