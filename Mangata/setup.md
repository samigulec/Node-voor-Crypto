<h1 align="center"> Mangata </h1>



## Link
 * [Mangata officieel website](https://mangata.finance/)
 * [Mangata officieel Twitter](https://twitter.com/MangataFinance)
 * [Mangata document](https://docs.mangata.finance/welcome/)
 


### Systeemvereisten


| ------------ | ------------ |
| ✔️CPU |	2+ vcpu|
| ✔️RAM	| 4+ GB |
| ✔️Storage	| 100+ GB SSD |
| ✔️UBUNTU | 20-22 |


### Docker setup
```
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
```
sudo apt-get update
```
```
sudo apt-get install ca-certificates curl gnupg
```
```
sudo install -m 0755 -d /etc/apt/keyrings
```
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
```
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
```
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
sudo apt update -y && sudo apt upgrade -y
```
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
### Go
```
ver="1.21.6"
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz"
rm "go$ver.linux-amd64.tar.gz"
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile
source $HOME/.bash_profile
go version
```

### EigenLayer

```
git clone https://github.com/Layr-Labs/eigenlayer-cli.git
```
```
cd eigenlayer-cli
```
```
mkdir -p build
```
```
go build -o build/eigenlayer cmd/eigenlayer/main.go
```
```
cd
sudo cp eigenlayer-cli/build/eigenlayer /usr/local/bin/
```

### Key maken

```
eigenlayer operator keys create --key-type ecdsa user
```
```
eigenlayer operator keys create --key-type bls user
```

### Key vervangen

```
eigenlayer operator keys list
```



### Operator aanmelden
```
eigenlayer operator config create
```

- y klikken.

- Operator adres is het Ethereum-adres in de output van de eerste transactie..

- Voer opnieuw het adres in dat u hierboven heeft ingevoerd.

- Goerli RPC is nodig, die we gratis verkrijgen via https://app.infura.io door een account aan te maken. OF probeer https://rpc.ankr.com/eth_goerli te gebruiken.

- `ecdsa key` doc  : /root/.eigenlayer/operator_keys/user.ecdsa.key.json

- goerli klikken.







### register

-We hadden bovenaan een sleutel gemaakt, er waren 2 codes, de uitvoer van de eerste bevat de private key. Voeg deze toe aan MetaMask. Het zal moeilijk zijn, maar vind een Goerli faucet... Voer voor de laatste transactie de onderstaande code in... de logs zullen een beetje stromen, wacht tot het klaar is..
```
eigenlayer operator register operator.yaml
```







### Document kopieren
```
git clone https://github.com/mangata-finance/avs-operator-setup.git
```
```
cd avs-operator-setup
```
```
chmod +x run.sh
```
```
nano .env
```


ETH_RPC_URL= infuradan alınan http linki

ETH_WS_URL= infuradan alınan wss linki

ECDSA_KEY_FILE_HOST=/root/.eigenlayer/operator_keys/user.ecdsa.key.json

BLS_KEY_FILE_HOST=/root/.eigenlayer/operator_keys/user.bls.key.json

ECDSA_KEY_PASSWORD=key

BLS_KEY_PASSWORD=key

- ctrl xy enter.

```
./run.sh opt-in
```
```
docker compose up -d
```
```
docker ps
```

```
docker logs -f --tail 100 docker-id
```
YADA
```
docker logs -f --tail 100 avs-finalizer-node
```

- Laat de logs een beetje lopen, neem dan een screenshot en gooi het in het avs-operators kanaal op Discord, ze zullen je een rol geven, genaamd Mangatarians. Er is ook een bot in hetzelfde kanaal, klik daarop om de node runner rol te krijgen. De Discord-link is te vinden bij de links aan het begin van de pagina.


#### Operator controleren
```
eigenlayer operator status operator.yaml
```
#### Update voor oparetor
```
eigenlayer operator update operator.yaml
```

### helemaal verwijderen

```
cd avs-operator-setup
```
```
docker compose down -v
```
```
cd 
rm -rf avs-operator-setup
rm -rf eigenlayer-cli
```


Dat was het <3