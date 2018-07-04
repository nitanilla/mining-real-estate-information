
# iMobPrime - React Frontend for a Real Estate Management App

This is a **React** project created with the [Create React App](https://github.com/facebookincubator/create-react-app) utility and contains only the `frontend` of a prototype for a `Real Estate Management Application`.

This frontend project is using Rest API endpoints from the project [imobprime-spring-boot](https://github.com/jorgealmeidajr/imobprime-spring-boot).

## Table of Contents

- [Introduction](#introduction)
- [Folder Structure](#folder-structure)
- [Available Scripts](#available-scripts)
- [Features](#features)
- [Missing Features to implement](#missing-features-to-implement)

## Introduction

This project was created to be used by `Real Estate Agents or Brokers` that have to manage many `Properties` for their `Clients`. Those `Real Estate Agents or Brokers` are associated and work with `Real Estates`. For this application there are `Clients` and their data are managed by `Real Estate Agents or Brokers`. There are `Clients or Owners` that have properties to sell or rent and `Clients Interested` in a `Property` to buy or rent.

This project is going to focus in the `Real Estate Agents or Brokers` necessities, they are going to be the main actor for this project. This application will provide an easy and fast way for `Clients Interested` in a `Property` to search properties to sell or rent.

## Folder Structure

The folder structure of the project looks like this:

```
imobprime-react/
  README.md
  package.json
  public/
  src/
    api/        -> Classes for REST API integration
    components/ -> React Components
    App.js
    index.js
```

## Available Scripts

In the root project directory, you can run:

### `npm start`

Runs the app in the development mode.<br>
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br>
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br>
See the section about [running tests](#running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br>
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br>
Your app is ready to be deployed!

## Features

### Home Page

This page is going to be public and accessed by anyone.

The image below is the initial page of the application. You can click in the search button in the left to filter properties by some parameters. You can search properties available to sell or rent in the input text typing the city name or district name. At the right there are two buttons that change the way to see the result of search, you can choose the map format default that uses Google Maps or the grid. 

Pagina inicial exibindo os imoveis em um mapa baseando-se na posicao(lat, lng) do cliente.
![home00](https://user-images.githubusercontent.com/6424524/35781245-b94b52dc-09ce-11e8-99a1-4a5f7a62e916.png)

Na pagina inicial eh possivel fazer uma pesquisa mais completa de imoveis usando varios parametros.
![home01](https://user-images.githubusercontent.com/6424524/35781260-f50cbc66-09ce-11e8-9e2b-b0820eeb0fff.png)

Listagem de imoveis no modo de Grid.
![home02](https://user-images.githubusercontent.com/6424524/35781278-2e605586-09cf-11e8-99e5-ac3d47e37f9e.png)

### Real Estates Page

This page is going to be accessed only by the `Administrator` of the application.

The image below is a printscreen of the `Real Estates` page that has CRUD functionalities. Here you can list all real estates, filter real estates by some parameters, create a new real estate, update or delete a real estate. 

![real-estates](https://user-images.githubusercontent.com/6424524/35781283-4ae93d12-09cf-11e8-84fb-623c01c93b8c.png)

### Real Estate Agents or Brokers Page

This page is going to be accessed only by the `Administrator` of the application.

The image below is a printscreen of the `Real Estates Agents or Brokers` page that has CRUD functionalities. Here you can list all real estate agents, filter real estates agents by some parameters, create a new real estate agent, update or delete a real estate agent. Here the administrator can activate or deactivate an `Real Estate Agent or Broker` account.

![agents](https://user-images.githubusercontent.com/6424524/35781284-5813ab26-09cf-11e8-9adc-c2769dc207a6.png)

### Clients Page

This page is going to be accessed by the `Administrator` and the `Real Estate Agent or Broker`.

The image below is a printscreen of the `Clients` page that has CRUD functionalities. Here you can list all clients, filter clients by some parameters, create a new client, update or delete a client.

![clients](https://user-images.githubusercontent.com/6424524/35781292-6d0833a8-09cf-11e8-8d74-f78c7593a227.png)

### Properties Page

This page is going to be accessed by the `Administrator` and the `Real Estate Agent or Broker`.

The image below is a printscreen of the `Properties` page that has CRUD functionalities. Here you can list all properties, filter properties by some parameters, create a new property, update or delete a property.

![imoveis](https://user-images.githubusercontent.com/6424524/35781307-818e3bc4-09cf-11e8-8f37-85beb50a6cae.png)

## Missing Features to implement

* Authentication security with JWT or other library;

* Authorization and access control with login and profile (admin and real estate agent);

* Internationalization (change the locales between english or brazilian portuguese);

* Improve database test and apply indexing;

* Add pagination and sorting capabilities in all data tables;

* Add mask in input fields that values need to be formatted;

* Inplace row editing in data tables(use this feature in simple fields like strings, not for combo boxes),

* Install redux for state management.

### Home TODOS

BUG: Busca de propriedades by params esta dando um erro, a url de request fica como '/city/null', null eh o id da cidade.

Clear search form na busca de imoveis by params.

Search by region in the input search.
	
### Real Estates TODOS

Nao esta sendo feito o upload da imagem do logo no create e no edit.

No listar deve-se mostrar a imagem do logo.

Refatorar o component Imobiliarias e rename to RealEstates.

### Agents TODOS

Falta ativar/desativar o corretor de maneira inplace na grid de listagem.

Clear form for create or edit agent.

No frontend e no backend preciso validar o CPF, CNPJ, phoneNumber, cellPhoneNumber, email e site informados.
Essas rotinas que serao implementadas podem ser usadas e outras telas nesse sistema.

### Clients TODOS

Um corretor vai possuir varios clientes.
Preciso planejar como vincular o corretor ao cliente. 
Hoje todo cliente fica vinculado ao um mesmo corretor de id = 1.
	
Preciso mudar o schema na coluna atributos na tabela cliente.
Hoje estado esta dentro de cidade.
Na coluna atributos teriamos o seguinte schema:
```
endereco: {
	cidade: {},
	estado: {}
}
```
Poderia aproveitar e renomear os campos do JSON para o ingles?
Essa modificacao afeta o cadastro e edicao de cliente, e afeta todos os dados na base de teste.
Seria necessario modificar as rotinas no imobprime-scripts.

No cadastro e na edicao, o campo cep/postalCode precisa tratar o erro quando nao existe o cep cadastrado na base de dados. 
Ele deve buscar o cep no ViaCep.

Clear form for create or edit client.

Na coluna atributos temos 'imoveis': [], 'tipo_cliente': 'interessado||proprietário'.
Esta faltando tratar esses campos no sistema.
Para o tipo de cliente basta colocar um radio button.
Falta planejar como associar imoveis a um cliente.

Falta planejar o que fazer com os combos de estado e cidade quando criar ou editar um cliente.

No campo de cep/postalCode so funciona quando o usuario digita o caractere '-'.
Ex: 88032600 nao funciona, 88032-600 funciona.
Isso pode afetar o cadastro de imobiliarias tambem.

### Properties TODOS

Vai ficar faltando vincular o endereco(uso o cep ou a rua?) a um ponto(lat, long).
Essa rotina usaria o GoogleMaps. Seria necessario alterar os dados da base de teste?
	
Nao esta sendo feito o upload da imagem. 
Deve ser possivel salvar varias imagens, a primeira imagem seria a principal.
Salvar as imagens em um diretorio na maquina/servidor, ou usar o Firebase ou o Amazon S3.
	
Esta faltando criar o PropertyEditModal component.
Foi feito o modal para create e delete, mas eles nao estao acessando o backend.
	
No create/edit falta definir como tratar o campo addressData JSON.
	
Search properties precisa ser refeito com spring jdbc template. 
Tive problemas com a coluna JSON usando native query em JPA.

