# ethereum-workshop

* установка необходимого софта
* запуск контракта, просмотр работы приложения
* написание кода
* деплой в основную тестовую сетку

## Установка необходимого софта
1. npm, node, truffle, truffle-default-builder
2. **ВНИМАНИЕ!!!** Чтобы демо работало надо иметь версию truffle 3.2.1 . Если у вас уже стоит truffle, то удалите другую версию: `npm uninstall -g truffle` и напишите в терминале: `npm install -g truffle@3.2.1` 
3. устаналиваем `truffle-default-builder` с помощью `npm install truffle-default-builder --save`
4. если вы все правильно сделали, то сделайте `truffle init, truffle migrate, затем truffle build и truffle serve` и откроете браузер по ссылке `localhost:8080`, в соседнем окне надо ввести: `testrpc`

For windows users
```
mkdir eth-test
cd eth-test
truffle init
truffle migrate

в другом окошке терминала
testrpc
```

Копируем проект на компьютер и клонируем ветку с заданием:
```
mkdir ethereum-workshop
cd ethereum-workshop
git clone https://github.com/misteraverin/ethereum-workshop.git
git checkout -b task2 origin/task2
```
https://github.com/ethereum/wiki/wiki/JavaScript-API#web3ethgetbalance
## Запускаем нашу программу
*Two Bash command line required. One is for running TestRPC and other for running commands below*
  - `cd ~/ethereum-workshop`
  - `rm -r build/` // clean truffle dev environment 
  - `truffle migrate`
  - Copy address from RealEstateRegistry output:
      - `Deploying RealEstateRegistry...`
      - `RealEstateRegistry: 0xd0957deff78e0f87d949c1a08464af9c6d34a75c`
  - `truffle console`
      - `var status = {0: 'Owned', 1: 'On Sale', 2: 'Await Confirmation'};`
      - `function printEstate(estate) {console.log(' - Real Estate with id ' + estate[0] + '\n\tname: ' + estate[1] + '\n\tprice: ' + web3.fromWei(estate[2], 'Ether') + ' eth\n\tstatus: ' + status[estate[3]] + '\n\towner: ' + estate[4], '\n\tpotential owner: ' + estate[5]); };`
      - `web3.eth.accounts`
      - `var seller = web3.eth.accounts[0];`
      - `var buyer = web3.eth.accounts[2];`
      - `var inspector = web3.eth.accounts[1];`
      - `var contract = RealEstateRegistry.at('0xd0957deff78e0f87d949c1a08464af9c6d34a75c');`  // put actual contract address
      - `contract.getEstate.call(1).then(function(estate) { printEstate(estate); });`
    
      - #### Put apartment #1 on sale:
      - `contract.sell(1,web3.toWei(10,'Ether'),{from:'0xaec3ae5d2be00bfc91597d7a1b2c43818d84396a', gas: 10000});`  // you could error for not enough GAS for the transaction 
      - `contract.sell(1,web3.toWei(10,'Ether'),{from:'0xaec3ae5d2be00bfc91597d7a1b2c43818d84396a', gas: 41494});`
      - `contract.getEstate.call(1).then(function(estate) { printEstate(estate); });`  //to see details of  estate ID #1 

      - #### Buy apartment #1:
      - `contract.buy(1, { from:buyer });`
      - `contract.getEstate.call(1).then(function(estate) { printEstate(estate); });`
      - #### Confirm the deal by inspector:
      - `contract.confirm(1, {from:buyer});`  //you could get error since only inspector can confirm
      - `contract.confirm(1, {from:inspector});`
      - `contract.getEstate.call(1).then(function(estate) { printEstate(estate); });`
      - `web3.eth.accounts`  // review addresses and check that the ownership was done correctly
  
## Написание кода
Get amount of money sent with current transaction:
```
uint256 amountReceived = msg.value;  // in Wei
```
Send money to somebody else:
```
address guy1 = 0xdeadbeef.....;
uint256 amountToSend = 10 ether;
guy1.send(amountToSend);
```

We've noticed that some of the tests do not work. The problem
that we do not really send any money from buyer to seller. Let's fix it!

We need to implement the following:
  - send money (ethers) with `buy` function call
  - validate that buyer sent correct amount (equal to apartment price)
  - send 95% of the price to the seller when inspector confirms the deal
  - send 5% to inspector as a fee
 
Make sure that all tests work now!

To edit code right on the serve use `nano` or `vim`

## Деплой в основную сетку
1. устанавливаем parity [link](https://github.com/paritytech/parity)
2. создаем аккаунт на [myetherwallet](https://www.myetherwallet.com/) в kovan testnet, сохраняем key-store file на компьютер
3. запускаем `parity-ui` и переходим в kovan testnet
4. импортируем аккаунт из key-store
5. чтобы получить 1 тестовый эфир: создаем gist на github с вашим адресом и пишем команду в терминале: `curl http://github-faucet.kovan.network/url --data "address=https://gist.github.com/[github_username]/[gist_hash]`, затем идем в https://kovan.etherscan.io/ и смотрим свои транзакции. Можно и другими способами: https://github.com/kovan-testnet/faucet
6. после того как тестовая сеть синхронизировалась мы запускаем `truffle migrate` и идем в parity клиент, чтобы подтвердить транзакции.<br>

Ремарка: тоже самое можно сделать, подняв рабочую через консоль или воспользоваться Infura
