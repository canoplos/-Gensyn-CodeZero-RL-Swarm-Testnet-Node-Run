# 🤖 Gensyn CodeZero RL Swarm Testnet Node Kurulum Rehberi


Bu rehber, **Gensyn**'in merkeziyetsiz bilgi işlem ağı üzerinde, **CodeZero RL Swarm Testnet** düğümünü (Node) başarıyla kurup çalıştırmanız için gerekli tüm adımları içermektedir.


---

## 🎯 Proje Hakkında: RL Swarm Testnet


**Gensyn**, yapay zeka eğitim ve çıkarımını merkezi olmayan bir şekilde sağlayan bir Katman-2 protokolüdür. **CodeZero RL Swarm Testnet** ise, dağıtık bir ortamda karmaşık **Pekiştirmeli Öğrenme (RL)** iş yüklerini çözerek ağın performansını test etmeyi amaçlayan kritik bir test aşamasıdır. Bir düğüm çalıştırmak, bu merkeziyetsiz yapay zeka devrimine erkenden katılmanızı sağlar.


---












<img width="750" height="450" alt="image" src="https://github.com/user-attachments/assets/f1877150-2235-4b0b-8c78-0fc3afa0c685" />














## 🛠️ Ön Koşullar





Lütfen kurulumdan önce aşağıdaki gereksinimlerin karşılandığından emin olun:

* **Git:** Depoyu klonlamak için gereklidir.
* **Python 3.8+:** Projenin çalışacağı temel ortamdır.
* **Donanım:** Testnet gereksinimlerine uygun minimum CPU, RAM ve Depolama alanı. (Lütfen resmi Gensyn Testnet dokümantasyonunu kontrol edin.)



##  Donanım Gereksinimleri 



 CPU & GPU Destekleniyor 




Sadece - CPU :  arm64 or x86 CPU with minimum 32gb ram (Eğitim sırasında başka uygulamalar çalıştırırsanız, eğitimin çökebileceğini unutmayın.).





VEYA


 ·  GPU :

 
   ·     RTX 3090
   ·     RTX 4090
   ·     RTX 5090
   ·     A100
   ·     H100           
   ·     ≥24GB vRAM GPU is recommended, 
   ·     ≥12.4 CUDA Driver.

        


---





## Adım 1: Depoyu Klonlama ve Hazırlık






1.  **Sistem Paketlerini Güncelleyin:**

    ```bash
    sudo apt update && sudo apt upgrade -y 
    ```





2.  **Genel Yardımcı Programları ve Araçları yükleyin**

    ```bash
    sudo apt install screen curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y
    ```





3.   **Python'u yükleyin:**

     ```bash
     sudo apt install python3 python3-pip python3-venv python3-dev -y
     ```




4.  **Node yükleyin:**

    ```bash
    sudo apt update
    curl -fsSL https://deb.nodesource.com/setup_22.x | sudo bash -
    sudo apt install -y nodejs
    node -v
    npm install -g yarn
    yarn -v
    ```


5. **Yarn'ı yükleyin**



   ```bash
   curl -o- -L https://yarnpkg.com/install.sh | bash
   ```



   ```bash
   export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"
    ```



   ```bash
   source ~/.bashrc
   ```

   
    


   


## Adım 2: HuggingFace Erişim belirtecini edinin  Mecburi değildir




1.  https://huggingface.co/    hesap oluşturun



2.  https://huggingface.co/settings/tokens     write ile   token oluşturun  












## Adım 3:  Depoyu Klonlayın


  ```bash
    git clone https://github.com/gensyn-ai/rl-swarm/
   ```























    

---

## Adım 2: Bağımlılıkları Yükleme (Install Dependencies) 📦

Sanal ortam aktifken, `requirements.txt` dosyasında listelenen tüm gerekli Python kütüphanelerini yükleyin.

1.  **Bağımlılıkları Yükleme Komutu:**

    ```bash
    pip install -r requirements.txt
    ```

    > ⚠️ **Not:** Yüksek performanslı hesaplama kütüphaneleri (örn. `torch`, `tensorflow`) büyük boyutlu olabilir ve GPU/CUDA uyumluluğu gerektirebilir. Yükleme sırasında hata alırsanız, ilgili kütüphanelerin resmi kurulum rehberlerini kontrol edin.

---

## Adım 3: Node Yapılandırması (Configuration) ⚙️

Gensyn düğümünüzü ağa bağlamak için API anahtarınızı veya cüzdan bilgilerinizi yapılandırmanız gerekir.

1.  **Örnek Dosyayı Kopyalama:** Depoda bulunan örnek yapılandırma dosyasını (`config.example.py` veya `.env.example`) kopyalayarak gerçek yapılandırma dosyanızı oluşturun:

    ```bash
    cp config.example.py config.py
    # Veya cp .env.example .env
    ```

2.  **Yapılandırma Dosyasını Düzenleme:** Oluşturduğunuz `config.py` (veya `.env`) dosyasını bir metin düzenleyici ile açın. Gensyn cüzdan bilgilerinizi, API anahtarınızı ve ağ bağlantı detaylarınızı ilgili alanlara girin.

    ```python
    # config.py içinden bir örnek
    GENSYN_WALLET_PRIVATE_KEY = "BURAYA_ÖZEL_ANAHTARINIZI_GIRIN"
    TESTNET_ENDPOINT = "wss://testnet.gensyn.ai/ws"
    ```

---

## Adım 4: Düğümü Başlatma (Running the Node) 🚀

Tüm bağımlılıklar yüklendi ve yapılandırma tamamlandıysa, düğümünüzü başlatmaya hazırsınız.

1.  **Node Başlatma Komutu:**

    ```bash
    python3 node_runner.py 
    # Veya projenin ana başlatma betiğinin adını kullanın.
    ```

2.  **Çalışmayı Onaylama:** Düğüm başarıyla başlatılırsa, terminalde ağa bağlandığını ve **"Waiting for RL tasks..."** (RL görevlerini bekliyor...) gibi bir mesaj gördüğünüzü teyit edin.

---

## 🛑 Düğümü Durdurma

Düğümün çalışmasını sonlandırmak için terminalde `Ctrl + C` tuş kombinasyonunu kullanın.

**Sanal Ortamdan Çıkış:** İşiniz bittiğinde sanal ortamdan çıkmayı unutmayın:

```bash
deactivate
