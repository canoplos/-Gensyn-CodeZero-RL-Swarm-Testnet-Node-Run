# 🤖 Gensyn CodeZero RL Swarm Testnet Node Setup Guide


This guide contains all the steps necessary to successfully set up and run the **CodeZero RL Swarm Testnet** node on **Gensyn**'s decentralized computing network.

---

## 🎯 About the Project: RL Swarm Testnet



**Gensyn** is a Layer-2 protocol that enables decentralized artificial intelligence training and inference. **CodeZero RL Swarm Testnet** is a critical testing phase that aims to test the network's performance by solving complex **Reinforcement Learning (RL)** workloads in a distributed environment. Running a node allows you to participate early in this decentralized artificial intelligence revolution.



---












![1500x500 (1)](https://github.com/user-attachments/assets/16a9e7f5-84ea-4996-a63a-b40f77c6f893)








---






## 🛠️  Pre requisites





Please ensure the following requirements are met before installation:


* **Git:** Required to clone the repository.
* **Python 3.8+:** This is the primary environment in which the project will run.
* **Hardware:** Minimum CPU, RAM, and storage space requirements compatible with Testnet specifications. (Please refer to the official Gensyn Testnet documentation.)





---



##   Hardware Requirements 




 CPU & GPU Supported 




Only - CPU: arm64 or x86 CPU with a minimum of 32GB RAM (Please note that running other applications during training may cause the training to crash.).





OR


 ·  GPU :

 
   ·  RTX 3090
   
   ·  RTX 4090
   
   ·  RTX 5090
   
   ·  A100
   
   ·  H100      
   
   
   ·  ≥24 GB vRAM GPU is recommended. 

   
   ·  ≥12.4 CUDA Driver.

        


---





## Step 1: Cloning the Repository and Preparation






1.  **Update System Packages:**

    ```bash
    sudo apt update && sudo apt upgrade -y 
    ```





2.  **Install General Utility Programs and Tools**

    ```bash
    sudo apt install screen curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y
    ```





3.   **Install Python:**

     ```bash
     sudo apt install python3 python3-pip python3-venv python3-dev -y
     ```




4.  **Install the node:**

    ```bash
    sudo apt update
    curl -fsSL https://deb.nodesource.com/setup_22.x | sudo bash -
    sudo apt install -y nodejs
    node -v
    npm install -g yarn
    yarn -v
    ```


5. **Load the yarn**



   ```bash
   curl -o- -L https://yarnpkg.com/install.sh | bash
   ```



   ```bash
   export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"
    ```



   ```bash
   source ~/.bashrc
   ```

   
    


   


## Step 2: Get the HuggingFace access token  Optional




1.  https://huggingface.co/    Create an account



2.  https://huggingface.co/settings/tokens     Create a token with write 












## Step 3: Clone the Repository


  ```bash
    git clone https://github.com/gensyn-ai/rl-swarm/
   ```




## Step 4: Run the Swarm





##  (GPU)





1-  Open a New Screen 

   ```bash
    screen -S swarm
   ```






2-  Enter the rl-swarm directory


   ```bash
    cd rl-swarm
   ```




---


3 - If you don't optimize VRAM, the 3090 GPU won't run the 1.5 model at all. 



   ```bash
    echo "Before:" && grep "dtype:" code_gen_exp/config/code-gen-swarm.yaml && sed -i "s/dtype: 'float32'/dtype: 'bfloat16'/" code_gen_exp/config/code-gen-swarm.yaml && echo "After:" && grep "dtype:" code_gen_exp/config/code-gen-swarm.yaml
   ```




---






4- Set up and run Swarm 


   ```bash
    bash run_rl_swarm.sh
   ```





## Step 5: Connecting email via tunneling




1-  Exit the previous screen with Ctrl + A D. Then create a new screen. 

 
     
   ```bash
    screen -S swarm
   ```



2-  Enter the rl-swarm directory




   ```bash
    cd rl-swarm
   ```



3-  Paste the code below and go to the website using the URL it provides. It will ask for your IP address; enter the server IP address as the password. It will accept it, then log in with your email.  




   ```bash
    npm install -g localtunnel
    lt --port 3000
   ```


4-  Press Ctrl + A, then D to exit, and please return to the previous screen using the following command:  


   ```bash
    screen -r  "screen numarası"
   ```      

      
    

## Final Steps  






1 -  After the installations are complete, in the final step, you will be asked hugginface y/N. If your internet speed is good, say hugginface y, but if it is poor, say N, otherwise the tours will not be completed.











2 - "if you don't perform this VRAM optimization "  It will ask you for the model name. There are two models available. If you are using the 3090 or 4090, press Enter or type the 0.5 model below and continue. If you have a 5090 or higher device, type the 1.5 model and press Enter. 






## Model names






**Qwen/Qwen2.5-Coder-0.5B-Instruct**




**Qwen/Qwen2.5-Coder-1.5B-Instruct**




---

## Node name






1 - Please copy your node name and peer ID. This is important.  “Your node name starts with ‘Hello’.  Copy and save that address and your peer ID. 





2 -  You can log in via email from here and check your points.  https://dashboard.gensyn.ai/









<img width="1141" height="368" alt="image" src="https://github.com/user-attachments/assets/0fd4db6a-a80c-4504-a041-60c6e9cbea73" />








---






---

## Finally, if there is a node, you want to update it.





1 -  While your node is running in the screen, stop it with ctrl + c and enter the following command 




   ```bash
    deactivate && rm -rf .venv && git stash && git pull && python3 -m venv .venv && source .venv/bin/activate && bash run_rl_swarm.sh
   ``` 





2 - Then restart it, your node is now updated.



 
   ```bash
    bash run_rl_swarm.sh
   ```  



---




