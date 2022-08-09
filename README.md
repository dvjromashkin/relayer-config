Complete instructions for setting up an IBC bridge between STRIDE-TESTNET-2 and GAIA

1.	Install Gaia

First, we need to deploy a GAIA network node somewhere. I do this on a separate virtual machine, but for those who like to fasten several Tendermint nodes to one node, you can try changing the ports.

First, let's use the quick installation of the node through the developers script

```wget https://github.com/Stride-Labs/testnet/raw/main/poolparty/gaia/join_gaia.sh  && chmod a+x join_gaia.sh && ./join_gaia.sh ```

We answer the questions: the name of the node, y , confirm the default path, or if you have it different, we correct it, at the end we refuse to immediately launch it with the letter “n” and press Enter.

Next, find out your IP. This can be done with the command:

``` curl ifconfig.io/ip ```

We need to replace this address in several files:

``` nano $HOME/.gaia/config/client.toml ```

We are looking for the line "node = "tcp://localhost:26657"" and instead of "localhost" we write our IP.

Save and exit with the key combinations “ctrl+s” and “ctrl+x”

``` nano $HOME/.gaia/config/config.toml ```

Looking for lines:

```
[rpc]
# TCP or UNIX socket address for the RPC server to listen on
laddr = "tcp://127.0.0.1:26657"
```

We replace 127.0.0.1 with our IP address.
Below in the line "external_address = """ in quotes we write our IP address and port: 26656
Even lower, we find the line “persistent_peers = 98ed4fbbaf04cb21076dcac959d91b2efa75d02c@gaia.poolparty.stridenet.co:26656” and delete it (you can delete a line in Nano by pressing the “ctrl + k” key combination), and instead of it we insert another line with a large set of peers:

```
persistent_peers = "98ed4fbbaf04cb21076dcac959d91b2efa75d02c@gaia.poolparty.stridenet.co:26656,100f7e8485c6bc672037140f13cadadd133a2a4e@116.202.227.117:23656,6b4c727574f2788611df9c342710beb2398721dd@213.202.212.155:23656,92cde3bd413af857c7b2bfcd896786cb76c9fb9b@80.209.240.103:23656,e6afa1f3481ad03b7e4a96de12354cfef3e6d9cb@159.223.152.53:23656,7f9c62bedb8d82859708537fb376a152aba8e5c7@147.182.143.14:23656,6b85c6a0b2cdcf05d0ce5b2f6a78728b510fcb01@131.255.179.4:23656,956eb0d9ca320f5fbd3cf787a6d01bd569c66cb1@40.69.144.224:23656,6db4fdb1090f78bfd70e5c282d20eb2fb048c3b1@20.2.71.19:23656,61bce0b1cab8e840a79e78c2c43301e73a258e20@40.76.186.18:23656,853174f1ca8b78fbbfdefd32af7cc1f3fc424ce3@185.182.187.33:23656,ac3e44fc61aa6f663205aa4d66594d5d59f71b80@65.108.76.44:11544,905b20ef84e5d228ee5a7293603ead6734bd1e5a@142.132.176.148:23656,f3f18b9bc8dcf10e77def54d2bab390d92b8e3e6@20.77.70.228:23656,aa3aa0e1244c0503b6d94d7a2ab4554ba0e3fd79@173.212.233.187:23656,2e79740ef74c0d61a872bca0b2780f95a600a144@20.24.67.9:23656,a64faaf6fe45425352524341d2f390ce6c603c09@139.162.2.113:23656,c0ba0b1561a82cc833f9c1ed490f7f769c99e37e@52.8.128.18:26656,28df1baca45a5c8a35804c4c3d39a7ec754c0bd7@178.18.248.69:23656,a5fcaa76d76c6812db176afb9c33e9ceeb4662e5@35.223.66.215:26656,b767515dca0be232fc287e0d274831a8c80fcac7@5.9.147.22:26256,ac141e35beefd50a553a09181b8643700c6c4545@104.208.80.139:23656,5674f7c078de9368b74b62b99920c9de8a80c359@113.161.82.243:23656,c3c32094135bc9d9148dbcbac52fdace8d01d62c@51.77.108.119:23656,bcb8420c5a3c67a9c4a4803c2a1d02d32f09eb8d@20.224.44.231:23656,0e604967eebb588654d7c417a9c02286d89d6037@89.163.215.204:11134,cf8339a43db4232cd781787bcb4f7641b8d1265e@167.71.196.118:23656,630461f5e87832375aa3a830a10da0d594d34f6e@194.163.168.99:23656,d31bfd43a027c0dc38a54799f4819c51a82c2d05@68.183.186.167:23656,9efd82081a07a2de802dc3e511185acafdcd425e@144.76.97.251:26766,b8948a13a8953f864ff43fa31ede14a21e44efdc@88.208.57.200:26656,192e7285369c526a7d8bd44c528e82e1a77699a9@20.194.250.123:23656,6a2e6300085ce12feb86f1206520e4e16cf03dd2@185.16.38.196:23656,a84b444bbcce26e9f279e5d8f3447af7ae30af62@34.123.180.250:23656,7e6f186ef11881ac3af87d6791ef834ba3128df6@139.59.121.134:23656,10776edaec11d981551ef5fecc1522fc541039d5@20.254.149.43:23656,5095dca3c7380e1bfea4cc0cdc136e17a0c79fd9@209.145.56.41:23656,d55982e5ed976dda2a04cf2a5b5c23b49a80bb92@188.166.241.251:23656,d5e7a8983f10e00c321b18532eab5a8cb7a3dcbc@86.48.0.222:23656,2b79dae3d3289a35d54973a4db35e2e0ade87bb7@65.108.238.183:23656,eb7060ffbff8dd4a4f029a386b3ca5e1c44f2b60@35.205.234.23:23656,489456b63a43d59673ddd65afcf174d30fcbb0d0@149.102.129.235:23656"
```

Save and exit (ctrl+s, ctrl+x)
Create a service file

``` nano /etc/systemd/system/gaiad.service ```

Paste the following

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
Save and exit (ctrl+s, ctrl+x)

Enable and start the service:

``` systemctl enable gaiad && systemctl start gaiad ```

Checking the logs:

``` journalctl -u gaiad -f -o cat ```

Please note that it may not start immediately, you just need to wait.

Be sure to wait for full synchronization.

2. Stride tuning

We repeat the procedure with the definition of IP, and remember it.

``` curl ifconfig.io/ip ```

Then we open the files and edit our IP

``` nano $HOME/.stride/config/client.toml ```

We are looking for the line "node = "tcp://localhost:26657"" and instead of "localhost" we write our IP.

Save and exit with the key combinations “ctrl+s” and “ctrl+x”

Open the following file:


``` nano $HOME/.stride/config/config.toml ```

Looking for lines:

```
[rpc]
# TCP or UNIX socket address for the RPC server to listen on
laddr = "tcp://127.0.0.1:26657"
```

We replace 127.0.0.1 with our IP address.

Below in the line "external_address = """ in quotes we write our IP address and port: 26656

Then at the very bottom we look for the line “indexer =” you should have the value “kv”, if it is “null” you need to fix it.

Save and exit (ctrl+s, ctrl+x)

Restart Stride:

``` systemctl restart strided ```

3. Installing Cosmos-relayer v2.0.0

Downloading the application:

``` wget https://github.com/cosmos/relayer/releases/download/v2.0.0-rc4/Cosmos.Relayer_2.0.0-rc4_linux_amd64.tar.gz ```

Unpacking:

``` tar  -zxvf Cosmos.Relayer_2.0.0-rc4_linux_amd64.tar.gz ```

Transferring:

``` mv "Cosmos Relayer" /usr/local/bin/rly ```

Next, we initialize:

``` rly config init ```

First, let's add a file with the necessary settings for the chain we need, for this, we write the command:

``` nano stride.json ```

Paste and edit: key – wallet name, rpc-addr – IP address of your Stride node.
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
Save, exit.

We do the same for the second chain:

``` nano gaia.json ```

We insert and edit the same way as the previous file, we only specify the IP address of the Gaia node.

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

Next, add our chains to Relayer

```
rly chains add --file=/root/stride.json stride
rly chains add --file=/root/gaia.json gaia
```

Then we add recovery keys, first on one network, then on another:

```
rly keys restore stride <your wallet moniker> "your mnemonic phrase"
rly keys restore gaia <your wallet moniker> "your mnemonic phrase"
```

Next, we check the performance of our setting by checking the balance:

```
rly q balance stride
rly q balance gaia
``` 

Next, you need to add the transfer path to the relayer, you just need to add the necessary lines to the config file. To do this, open the config file:

```
nano $HOME/.relayer/config/config.yaml
```

and replace the line "paths: {}" with:

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
                - channel-12
                - channel-2
                - channel-3
                - channel-4
```

check our setup with the command:

```
rly paths list
```

If everything is ok, we proceed to create a service file:

```
nano /etc/systemd/system/relayer.service
```

Insert:

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

Save, exit, enable/start the service:

```
systemctl enable relayer && systemctl start relayer
```

Checking the logs

```
journalctl -u relayer -f -o cat
```

