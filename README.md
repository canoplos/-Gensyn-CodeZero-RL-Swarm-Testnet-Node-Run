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

 
   ·  RTX 3090
   
   ·  RTX 4090
   
   ·  RTX 5090
   
   ·  A100
   
   ·  H100      
   
   
   ·  ≥24 GB vRAM GPU önerilir. 

   
   ·  ≥12.4 CUDA Driver.

        


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




## Adım 4:  Run the Swarm





##  (GPU)





1-  Yeni Bir Screen açın 

   ```bash
    screen -S swarm
   ```






2- rl-swarm dizinine girin


   ```bash
    cd rl-swarm
   ```





3- Swarm'ı kurun ve çalıştırın 


   ```bash
    bash run_rl_swarm.sh
   ```





## Adım 5:  Tünelleme ile mail bağlama 




1-  önceki screen'den ctrl + a d ile çıkın  sonra yeni bir screen oluşturun 

 
     
   ```bash
    screen -S swarm
   ```



2-  rl-swarm dizinine girin




   ```bash
    cd rl-swarm
   ```



3-  Bu aşşağıdaki kodu yapıştırın ve size verdiği url ile websiteye gidin sizden ip istiyecek şifre olarak sunucu ip'sini verin kabul edecek sonra mail ile giriş yapın 




   ```bash
    npm install -g localtunnel
    lt --port 3000
   ```


4-  Ctrl + A  D   ile çıkın ve aşşağıdaki komutla önceki screen'e dönün lütfen  


   ```bash
    screen -r  "screen numarası"
   ```      

      
    

## Son Adımlar 






1 -  Kurulumlar bittikten sonra  son adımda sizden hugginface y/N diyecek eğer internet hızınız iyiyse  hugginface  y diyin ama kötüyse N diyin yoksa turları yetişemiyor











2 -  Sizden model ismi isteyecek zaten 2 tane model var eğer 3090 ve 4090 kullanıyorsanız enter basıp yada aşşağıdaki 0.5 modelini yazıp devam edebilirsiniz yada 5090 ve üstü cihazınız varsa 1.5  modelini yazın ve enter basın 






## Model isimleri






**Qwen/Qwen2.5-Coder-0.5B-Instruct**




**Qwen/Qwen2.5-Coder-1.5B-Instruct**






## Node Adı 






1 - Lütfen node adınızı ve peer id'nizi kopyalayın bu önemlidir  " Hello'dan başlayan node adınızdır  ve peer id o adresi kopyalayın ve kaydedin "





2 -  Burdan mail ile bağlanıp puanlarınıza bakabilirsiniz  https://dashboard.gensyn.ai/












## Son olarak eğer node varsa güncellemek istiyorsanız





1 -  node'nuz  screen içinde çalışırken ctrl + c ile durdurun ve aşşağıdaki komutu girin 




   ```bash
    deactivate && rm -rf .venv && git stash && git pull && python3 -m venv .venv && source .venv/bin/activate && bash run_rl_swarm.sh
   ``` 





2 - Sonra tekrar çalıştırın artık node'nuz güncellendi 



 
   ```bash
    bash run_rl_swarm.sh
   ```  








