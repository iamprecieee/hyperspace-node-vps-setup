## Requirements
- KVM-based VPS service e.g. [Linode](https://cloud.linode.com/linodes)
- Termius mobile/desktop app
- Subscription fee (min $24 if using linode; not charged upfront, but billed hourly)
- Hyperspace private key


## VPS Setup (Linode)
- Create or log into linode account.
- In the "Linodes" section, select "Create Linode".
- Select preferred region and OS (Ubuntu 24.04 LTS).
- Choose a linode plan (min 8GB recommended on **SHARED CPU**).
- Enter your root password.
- That's all, press "Create Linode" button at the buttom.
- Once created and provisioned successfully, you will see your public IP and SSH details.


## Termius Setup
- Open and login to your termius app (select "starter" plan if prompted).
- Click on "New Host".
- Enter your linode public IP in the address box.
- Enter a name for your host in the general label box e.g. hyperspace.
- Enter "root" in the username box.
- Enter your root password in the password and press thee "Connect" button.


## Node Setup
- Install necessary dependencies:
    ```bash
    sudo apt update && sudo apt install -y git curl build-essential pkg-config libssl-dev git-all wget screen && sudo rm -rf /var/lib/apt/lists/*
    ```
- Install aiOS cli:
    ```bash
    curl https://download.hyper.space/api/install | bash
    ```
- Start cli in a new screen (background):
    ```bash
    screen -S aios
    aios-cli start
    ```
- Press `CTRL+A+D` to detach from screen.
- Install model depending on your allocated RAM (larger models == more GPU memory == more points) e.g. for 8 GB RAM:
    ```bash
    aios-cli models add hf:bartowski/Qwen2.5-Coder-14B-Instruct-GGUF:Qwen2.5-Coder-14B-Instruct-Q8_0.gguf
    ```
- Create a `.pem` file:
    ```bash
    nano ./key.pem
    ```
- Paste your hyperspace private key.
- Press `CTRL+X`, press `Y`, then press `Enter` to save file and exit.
- Load your key from file:
    ```bash 
    aios-cli hive import-keys ./key.pem
    ```
- Login and connect to network:
    ```bash
    aios-cli hive login
    aios-cli hive connect
    ```
- Select tier based models and GPU memory:
    ```bash
    aios-cli hive select-tier 3
    ```


---

- To check multiplier and points:
    ```bash
    aios-cli hive points
    ```
- To check your current keys:
    ```bash
    aios-cli hive whoami
    ```
- To check existing screens:
    ```bash
    screen -ls
    ```
- To reopen a detached screen:
    ```bash
    screen -r <screen_name> 
    ```
    e.g. ```screen -r hyperspace```
