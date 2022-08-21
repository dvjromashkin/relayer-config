Полная инструкция по натсройке IBC моста между STRIDE-TESTNET-2 и GAIA

1.	Запуск Gaia

Для начала,  нам нужно где-то развернуть ноду сети GAIA. Я это делаю на отдельной виртуальной машине, но для любителей прикрутить несколько нод Тендерминта на одну ноду, можете попробовать изменив порты.

Для начала воспользуемся быстрой установкой ноды через скрипт разработчиков

```wget https://github.com/Stride-Labs/testnet/raw/main/poolparty/gaia/join_gaia.sh  && chmod a+x join_gaia.sh && ./join_gaia.sh ```

Отвечаем на вопросы: имя ноды, y , подтверждаем умолчательный путь, или если он у вас иной – правим, в конце отказываемся от немедленного запуска буквой “n” и жмём Enter.

Далее узнаём свой IP. Это можно сделать командой:

``` curl ifconfig.io/ip ```

Данный адрес нам нужно заменить в нескольких файлах:

``` nano $HOME/.gaia/config/client.toml ```

Ищем строчку «node = "tcp://localhost:26657"» и вместo “localhost” пишем наш IP. 

Сохраняем и выходим комбинациями клавиш “ctrl+s” и “ctrl+x”

``` nano $HOME/.gaia/config/config.toml ```

Ищем строчки: 

```
[rpc]
# TCP or UNIX socket address for the RPC server to listen on
laddr = "tcp://127.0.0.1:26657"
```

Заменяем 127.0.0.1 на наш IP адрес.
Ниже в строчке «external_address = ""» в кавычках пишем наш IP адресс и порт :26656
Еще ниже, находим строчку «persistent_peers = 98ed4fbbaf04cb21076dcac959d91b2efa75d02c@gaia.poolparty.stridenet.co:26656» и удаляем её (удалить строчку в Nano можно комбинацией клавишь “ctrl+k”), а вместо её вставляем другую строку с большим набором пиров:
```
persistent_peers = "86d8c7991b6cd8223250859c6c8ec91fe6beb528@34.71.22.241:26656,3237468eae4eda47a5b3a05fb1f1758d55a9bb29@116.202.227.117:23656,3d516329bdf3ff13178bf0c094384200f29bbd36@65.109.31.7:23656,5011e2778cb49b9ae800d671e43802b252b9fbe6@78.107.234.44:36656,465547a24c21d8ae4d80d2b688766c13a35a726d@135.181.202.21:23656,214bfdf818aaa25f999295f471b5c16cc7d0f438@34.88.169.86:23656,bd531fc26b827bc0b6dc5afd2b1a816256629df4@95.216.208.37:23656,c31b962022031e1edd34b0a395a8338fb8062180@38.242.156.249:23656,614807fff2c881c93541cef8105576ea89b32e8f@108.214.8.13:26656,4b4c18d6206da1d82e71dbc1ea21e035eb8f47df@173.249.5.56:23656,a7ecee9a43a16684b09559ef0f872ea36445e37e@38.242.255.223:23656,015254cc413cd447266554162bf35b1881703cfe@194.233.67.89:23656,d448250c04d6ff486db951c1b5e8085ff648ae3e@38.242.139.54:23656,7df15bad855e3ef9e95fab3602872533be6b26ee@5.161.78.112:26656,3c117038682bbd1cc87ae98c802c8bd701601cf7@195.68.159.61:36656,a27d91d3b8b3e42d72aeba1d4e1bbce38a9e5b09@213.246.39.33:23656,2d5cdf2a7456dd66b7a405264b9d16adafd66111@38.242.243.214:23656,c758740c8858c4cfefd8ceab9ce4ef6e92b234ca@38.242.215.137:23656,e37a70c1101b675c7eb27e33a80744b38b914466@144.91.76.134:23656,3f114c69d53168044431409a7cd9e6f5869f7586@209.126.83.20:23656,e209ec56f78dcf7c8c56862cefd7c19ef5e81c99@173.212.243.149:23656,98cecf5159d47714a219ed500e36ff2f70d2b977@20.94.46.231:23656,25819455351465ad33d79af1691d1ce187b0b2c9@157.245.68.255:23656,3a1e40fe54ba08c9cc3a3acfa233e28fc2ae4827@194.163.158.47:23656,4dd0b3b158913aadb6ce856ec5b26337e3855a18@135.181.248.69:36656,23bcc603002fc8c920a7dcfa94e9541cb4e7742a@185.144.99.99:26656,39caee8d612556e4c194f0cf5c76773869717f05@38.242.156.245:23656,1fb0892581455b14990238b09e4ee928c9ad57be@38.242.225.140:23656,789ae52e1ef1047a73a8f64b8eb3fc2bb54f8ed0@65.21.254.161:23656,6ed9e5186b6fc4a265fe9acf1a4d8b921d2b162d@20.124.103.118:23656,3d8764b50d7552766bb9db60f1cc84e62a8c0f22@65.108.83.217:23656,4fa7318b927deb1f8631ad2f5990bd07c0f966a0@194.180.176.198:23656,111f2f9ccc0b9e1b40b5cc353fea2c7ec48821ca@38.242.156.248:23656,6ef555f981b06d94c0aa900700db4bb10e5f11cc@5.161.106.96:23656,644dd2cc35437c885ddc608c6c0cbe5a4de345ad@161.97.145.238:23656,3164e7912389d6a2a5ef4589ba9d1b427e6bf601@206.189.59.104:23656,3e251b5b2cdff234f5b976887f8f402bbfa1a920@185.197.75.47:23656,0c7556ab80727b4f209ac42af388e7c74d74921f@45.67.216.77:23656,ce2e3cc68afee1e6ce98d8e24ac142593137fbe2@38.242.215.136:23656,2b43910f82d55dc1ad2744658d4a0e2bf4b21f98@95.216.220.64:23656,1506b61367bd13a8c0b5f65f26085f12f67a92ae@135.181.33.148:23656,08715d04f58f3c6c3f7d75c445bc18654f722171@20.11.16.72:23656,776a92b8fe95690bc96efffa71115eee66c0129f@20.46.161.186:23656,94b35401f1e9c6a01e0d19b0b4a0baf6371ad62a@185.169.252.53:23656,e7ac3323bc111ac5b8b3645033741c21d1c1d902@144.91.84.105:23656"
```
Сохраняем и выходим (ctrl+s, ctrl+x)
Создаём сервисный файл
``` nano /etc/systemd/system/gaiad.service ```
Вставляем следующее
```
[Unit]
Description=Gaia Node
After=network.target
[Service]
Type=simple
User=root
ExecStart=/root/go/bin/gaiad start
Restart=on-failure
RestartSec=10
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
```

Сохраняем и выходим (ctrl+s, ctrl+x)

Включаем и запускаем сервис:

``` systemctl enable gaiad && systemctl start gaiad ```

Проверяем логи:

``` journalctl -u gaiad -f -o cat ```

Учтите, может не сразу запустится, нужно просто подождать.

Обязательно нужно дождаться полной синхронизации.

2.	Подстройка Stride

Повторяем процедуру с определением IP , и запоминаем его.

``` curl ifconfig.io/ip ```

Затем открываем файлы и редактируем наш IP

``` nano $HOME/.stride/config/client.toml ```

Ищем строчку «node = "tcp://localhost:26657"» и вместo “localhost” пишем наш IP. 

Сохраняем и выходим комбинациями клавиш “ctrl+s” и “ctrl+x”

Открываем следующий файл:


``` nano $HOME/.stride/config/config.toml ```

Ищем строчки: 

```
[rpc]
# TCP or UNIX socket address for the RPC server to listen on
laddr = "tcp://127.0.0.1:26657"
```

Заменяем 127.0.0.1 на наш IP адрес.

Ниже в строчке «external_address = ""» в кавычках пишем наш IP адресс и порт :26656

Затем в самом низу ищем строчку «indexer =» у вас должно быть значение “kv”, если стоит “null” нужно поправить.

Сохраняем и выходим (ctrl+s, ctrl+x)

Перезагружаем Stride:

``` systemctl restart strided ```

3.	Установка Cosmos-relayer v2.0.0

Скачиваем приложение:

``` wget https://github.com/cosmos/relayer/releases/download/v2.0.0-rc4/Cosmos.Relayer_2.0.0-rc4_linux_amd64.tar.gz ```

Распаковываем:

``` tar  -zxvf Cosmos.Relayer_2.0.0-rc4_linux_amd64.tar.gz ```

Переносим:

``` mv "Cosmos Relayer" /usr/local/bin/rly ```

Далее инициализируем:

``` rly config init ```

Для начала добавим файлик с нужными настройками нужной нам цепочки, для этого, пишем команду:

``` nano stride.json ```

Вставляем и редактируем: key – название кошелька, rpc-addr – IP-адрес вашего узла Страйд.

``` 
{
  "type": "cosmos",
  "value": {
    "key": "<your wallet moniker>",
    "chain-id": "STRIDE-TESTNET-2",
    "rpc-addr": "http://<your IP address>:26657",
    "account-prefix": "stride",
    "keyring-backend": "test",
    "gas-adjustment": 1.2,
    "gas-prices": "0.001ustrd",
    "debug": true,
    "timeout": "20s",
    "output-format": "json",
    "sign-mode": "direct"
  }
}
```

Сохраняем, выходим.

Делаем аналогично вторую цепочку:

``` nano gaia.json ```

Вставляем и редактируем аналогично прошлому файлу, только указываем IP адрес ноды Gaia.

```
{
  "type": "cosmos",
  "value": {
    "key": "<your wallet moniker>",
    "chain-id": "GAIA",
    "rpc-addr": "http://<your IP address>:26657",
    "account-prefix": "cosmos",
    "keyring-backend": "test",
    "gas-adjustment": 1.2,
    "gas-prices": "0.001uatom",
    "debug": true,
    "timeout": "20s",
    "output-format": "json",
    "sign-mode": "direct"
  }
}
```

Далее добавляем наши сетки в Релейер

```
rly chains add --file=/root/stride.json stride
rly chains add --file=/root/gaia.json gaia
```
Затем добавляем ключи восстановления, сначала в одной сети, потом в другой:

```
rly keys restore stride <your wallet moniker> "ваша мнемоника"
rly keys restore gaia <your wallet moniker> "ваша мнемоника"
```

Далее проверяем работоспособность нашей настройки при помощи проверки баланса:

```
rly q balance stride
rly q balance gaia
``` 

Далее нужно добавить путь трансфера в релейер, нужно просто дописать нужные строчки в конфиг файл. Для этого открываем конфиг файл:
```
nano $HOME/.relayer/config/config.yaml
```

и заменяем строчку « paths: {} » на:

```
paths:
    stride-gaia:
        src:
            chain-id: STRIDE-TESTNET-2
            client-id: 07-tendermint-0
            connection-id: connection-0
        dst:
            chain-id: GAIA
            client-id: 07-tendermint-0
            connection-id: connection-0
        src-channel-filter:
            rule: allowlist
            channel-list:
                - channel-0
                - channel-694
                - channel-2
                - channel-3
                - channel-4
```
проверяем нашу настройку командой:

```
rly paths list
```
Если всё ok, переходим к созданию сервисного файла:

```
nano /etc/systemd/system/relayer.service
```

Вставляем:

```
[Unit]
Description=relayer
After=network.target
[Service]
Type=simple
User=root
ExecStart=/usr/local/bin/rly start stride-gaia -d
Restart=on-failure
RestartSec=10
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
```

Сохраняем, выходим, включаем/запускаем сервис:

```
systemctl enable relayer && systemctl start relayer
```

Проверяем логи

```
journalctl -u relayer -f -o cat
```

