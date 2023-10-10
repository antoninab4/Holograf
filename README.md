# Holograph

## discord
https://discord.gg/holograph

## Установка оператора Holograph

### Думаем хватит и такого, но надо тестить 
### 2 GB RAM
### 2 vCPU
### 40SSD

# Установка 
## Начинаем как обычно с обновления сервера
```
sudo apt update && sudo apt upgrade -y
```

## Устанавливаем различные зависимости
```
sudo apt install make clang git pkg-config libssl-dev build-essential git gcc chrony curl jq ncdu bsdmainutils htop net-tools lsof fail2ban wget screen -y
```

## Устанавливаем npm и nodejs
```
curl -fsSL https://deb.nodesource.com/setup_current.x | sudo -E bash - 
sudo apt-get install -y nodejs
```

## Устанавливаем Holograph cli

```
npm install -g @holographxyz/cli
```

## Создаем конфиг с помощью недавно установленной cli

```
holograph config
```

## Далее нам необходимо будет ответить на вопросы:

### Which networks do you want to operate?
###  goerli
 ### mumbai
  ### fuji
   ### rinkeby - не работает

## Тут необходимо выбрать одну или несколько сетей, мы выбрали goerli, mumbai, fuji, забегая вперед, единственный фактор - селфстейк, в некоторых сетях он меньше 

### Enter the provider url for  goerli/mumbai/fuji

Для goerli и fuji просто жмем enter, для mumbai необходимо вписать другой ендпоинт, у нас он не работал 
Mumbai endpoint:
https://polygon-testnet.public.blastapi.io
Если ни один ендпоинт впоследствии не работает (как менять руками будет показано позже) идем и ищем рабочие сюда:
https://chainlist.org/

### Default private key to use when sending all transactions

Тут все просто, вписываем ваш приватник от кошелька, который вы создали специально для тестнета и идем дальше

### Please enter the password to encrypt the private key with

Вписываете пароль и на этом настройка вашего конфига заканчивается! 

## Что бы найти ваш недавно созданный конфиг идем по пути:
```
cd $HOME/.config/holograph/
```

В этой директории будет лежать файл config.json, можете его открыть и посмотреть, что там находится, тут же можно изменить ендпоинты вручную, в строках providerUrl, если это необходимо 

```
apt install nano
```
```
nano config.json
```
В этом пункте вам необходимо зафандить свои кошельки, монетами тех сетей, которые вы выбрали что бы получить токены $HLG для вашего оператора, ниже будут приведены ссылки с кранами, их великое множество можете сами поискать, если какие-то из них не работают

Для Goerli:
https://testnet-faucet.com/goerli/

Для Mumbai:
https://faucet.polygon.technology/

Для Fuji:
https://core.app/tools/testnet-faucet/?subnet=c&token=c

Далее переходим к функции cli faucet

```
holograph faucet
```
Тут будут простые вопросы, на которых я не буду зацикливать внимание, просто прочитайте, что от вас требуют, главное в конце увидеть зеленую надпись:

``
Request for tokens on goerli has been granted. You can return to request more tokens in 24 hours. Enjoy! 🤑
``

Поскольку кран дает 100 $HLG в сутки, для каждой сети, а вам 100% потребуется > 100 монет для поднятия оператора, для любой из предложенных сетей, на этом пункте вы можете остановиться до следующего дня, поскольку дальше продвинуться вы не сможете 


Как только у вас появилось ≧ 200 токенов $HLG, приступаем к следующему пункту - связываем наш кошелек с будущем оператором, создаем новую сессию в screen 

```
apt install screen
```
```
screen -S holograph
```

Связываем кошелек с оператором

```
holograph operator:bond
```

И снова вопросы, на которых сильно акцентировать внимания мы не собираемся, нужно лишь их прочесть и понять, что от вас требуется и в конце увидеть такую надпись, но с вашими переменными:

``
Welcome operator! 
Your wallet 0x... has bonded X eth to pod X on goerli/mumbai/fuji
Again please make sure your operator remains operational! Failure will result in slashed funds!
``

# Оставлю тут небольшую памятку об утилите screen:

``
#Выйти из screen, не завершая сессию 
``

``
ctrl + a + d
``

``
#Зайти обратно в уже созданную нами сессию
``

``
screen -x holograph
``

``
#Посмотреть существующие сессии
``

``
screen -list
``

# А тут будет небольшая памятка о Holograph cli:

``
#Рестарт вашей ноды, если она легла (подразумевается, что вы уже находитесь в screen)
``

``
holograph operator:bond
``


``
#запросить монеты с faucet-а
``

``
holograph faucet
``

``
#Бридж nft
``

``
holograph bridge
``

``
#Создание контракта
``

``
holograph create:contract
``

Если интересует более подробное объяснение команд и в целом, как работает holograph, велком в документацию https://docs.holograph.xyz/developer/welcome
