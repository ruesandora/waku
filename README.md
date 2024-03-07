<h1 align="center"> Waku </h1>

> Ne kadar sürecek? Bilgi yok - Ödüllü mü? Net değil olabilir. Garanti bir şey beklemiyorum, zaten kücük bir donanım.

> Neden kuruyorum? Proje katılmaya değer, vaktimi almadı, bir kaç dakikada kuruluyor.

> Topluluk kanalları: [Twitter](https://twitter.com/Ruesandora0) - [Duyuru](https://t.me/RuesAnnouncement) - [Chat](https://t.me/RuesChat) - [WP](https://whatsapp.com/channel/0029VaBcj7V1dAw1H2KhMk34) - [Node soruları için](https://t.me/ruesshare/13003/13004) - [Waku Discord](https://discord.gg/4DBrFfyY)

<h1 align="center"> Donanım </h1>

> Firma olarak [Hetzner](https://github.com/ruesandora/Hetzner/blob/main/README.md) kullanıyorum - siz kendinize göre seçebilirsiniz.
```
2 CPU 2 RAM - 40 SSD
```

<h1 align="center"> Kurulum </h1>

```console
# Sunucu güncellemesi ve gerekli paketler
sudo apt update && sudo apt upgrade -y
sudo apt-get install build-essential git libpq5 jq -y

# kodu girdikten sonra 1 seçelim.
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source "$HOME/.cargo/env"

sudo apt install docker.io -y
sudo curl -L "https://github.com/docker/compose/releases/download/v2.24.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
```console
# Waku kurulumu

# wakuyu klonluyoruz
git clone https://github.com/waku-org/nwaku-compose
cd nwaku-compose
cp .env.example .env

# .env içine giriyoruz bu komutla
nano .env
```

> Değiştireceğimiz kısımlar bunlar aşağıya yazıyorum:

* `ETH_CLIENT_ADDRESS` = Infura'dan Sepolia RPC aldım bedava onu ekledim - https://www.infura.io/
* `ETH_TESTNET_KEY` = Waku için açtığım metamaskın private keyini ekledim - Metamask hesap bilgileri kısmında
* `RLN_RELAY_CRED_PASSWORD` = Bir şifre belirledim

> CTRL X Y ENTER ile kaydedip çıkıyoruz.

```console
# ve register edelim.
./register_rln.sh
# register etmeden önce cüzdanda sepolia eth olmalı
```

<h1 align="center"> Waku node başlatma </h1>

```console
# portları açma

# yes diyelim bu komutu girdikten sonra
sudo ufw enable

# bu port komutlarını toplu girebilirsiniz.
sudo ufw allow 22    
sudo ufw allow 3000   
sudo ufw allow 8545   
sudo ufw allow 8645   
sudo ufw allow 9005   
sudo ufw allow 30304  
sudo ufw allow 8645

# docker up edelim
docker-compose up -d

# bu komutlar ile kontrol edebilirsin logları
docker-compose ps
docker-compose logs nwaku
```
```console
# bu komut ile içersine girelim:
nano ~/nwaku-compose/docker-compose.yml
```
> içersine girdikten sonra `ctrl w` yaparak `3000:3000` yazıp aratalım

> `127.0.0.1:3000:3000` olanı `0.0.0.0:3000:3000` şeklinde değişelim.

> CTRL X Y ENTER ile kaydedip çıkalım.

```console
# tekrar başlatalım
docker-compose down
docker-compose up -d
```

> Yaklaşık 1 saat içersine verileriniz güncellenecek

> `http://IP_ADRESİN:3000/d/yns_4vFVk/nwaku-monitoring`

> IP_ADRESİN kısmını değiştirip google'da aratın.

> Yedekleme için `keystore.json` dosyasını kaydedin.

```console
# Bu iki komutlada çıktı alıyorsanız sorun yoktur.
curl --location 'http://127.0.0.1:8645/debug/v1/version'
curl --location 'http://127.0.0.1:8645/debug/v1/info'
```



