


# ilk yapacağın şey
- öncelikle kayıt olun kurulumlar sonra baslayın. birden fazla kurabilirsiniz. kayır olduktan sonra kurulumu yapıp link alınca kayıt etmesi daha kolay oluyor. bu yüzden linkten kayıt olun giriş yapın profilden SOL cüzdanıda bağlayın sonra kurulumları yapın tık tık register edersiniz. ben bunu mutudan duymuşem kurulumuda o hazırlamış ben bir kaç düzeltme ve port değiştirme ekledim bu yüzden yazdım. 

https://app.blockcast.network?referral-code=ICoLxb

## 1️⃣ Sistem Güncelleme ve Gerekli Paketlerin Kurulumu
```
sudo apt update && sudo apt upgrade -y
sudo apt install -y ca-certificates curl gnupg lsb-release git
```
```
ufw allow 8080
ufw allow 8080/tcp
ufw allow 8089
ufw allow 8089/tcp
```
## 2️⃣ Docker ve Docker Compose Kurulumu
```
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
```
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
```
docker --version
```
## 3️⃣ dosyaları çek
```
git clone https://github.com/Blockcast/beacon-docker-compose.git
cd beacon-docker-compose
```
NOT: ağam paşam port değiştiriceğim ben diyorsan. bi aşağıdakinide yapıcan yoooooo değişmeyem diyorsan alttakini geç. port değişikliği 8080den 8089 ayarladım değiştiricekseniz docker compose yml içinden 8089 değiştir ama onun için portuda açmayı unutma.
```
curl -o $HOME/beacon-docker-compose/docker-compose.yml https://raw.githubusercontent.com/molla202/Block-cast/refs/heads/main/docker-compose.yml
```


## 4️⃣ Docker Container’ı Başlat
```
docker compose up -d
```

## 5️⃣ Node Kimliği Oluştur
```
docker compose exec blockcastd blockcastd init
```
Bu komut sana şunları verecek:

* Hardware ID
* Challenge Key
* Register URL

### Örnek:

* Hardware ID: csadsad-sad-sa-d-sa-dad-a
* Challenge Key: sadadsadnyhs67dsjad
* Register URL : https://app.blockcast.network/register?hwid=...

## 6️⃣ Node Kayıt Et

1. Tarayıcıda Register URL bağlantısını aç.
2. Konum izni isteyebilir → izin ver.
3. "Register" butonuna tıkla.
4. Kayıt başarıyla tamamlandığında node paneline yönlendirilirsin.

Panel: https://app.blockcast.network/manage-nodes

## 7️⃣ Node Durumu ve Kontrol

* Status: Online görünüyorsa kurulum başarılıdır.
* Multicast: “Not Enabled” olabilir, bu özellik daha sonra etkinleşir veya ağın izin vermesi gerekir.

## 🔄 Node’u Güncelleme (İleri Seviye)
```
cd beacon-docker-compose
git pull origin main
docker compose down
docker compose up -d
```
