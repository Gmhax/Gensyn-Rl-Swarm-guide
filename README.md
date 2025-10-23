# 💻 Gensyn AI RL-Swarm + Block Assist Complete Linux Guide

## Comprehensive setup guide for Gensyn AI  includes full instructions for RL-Swarm node, Telegram alerts, Swarm role verification, and Block Assist role completion via Octa.Space.


🖥️ System Requirements
| Resource | Minimum                    | Recommended         |
| -------- | -------------------------- | ------------------- |
| CPU      | 6 cores                    | **12 cores or more** |
| RAM      | 16 GB                       | **24 GB**           |
| Storage  | 100 GB SSD                 | **200–500 GB SSD**  |
| OS       | Ubuntu  24.04 (x64)        | Latest LTS          |


-  [Buy VPS here (Contabo)](https://contabo.com/en/storage-vps/storage-vps-30/?image=ubuntu.332&qty=1&contract=12)


🧱 Pre-Requirements

1️⃣ Update and Install Dependencies
```
sudo apt update && sudo apt install -y python3 python3-venv python3-pip curl wget screen git lsof ufw
```

2️⃣ Install Node.js, npm & Yarn
```
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update && sudo apt install -y yarn
```
- Check versions
```
node -v
npm -v
yarn -v
```

3️⃣Add 16 GB Swap to prevent Terminated
```
sudo fallocate -l 16G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```
- Verify swap
```
free -h
```
🚀 Run Gensyn RL-Swarm Node
1️⃣ Create a Screen Session
```
screen -S gensyn
```
2️⃣ Clone the Repository
```
git clone https://github.com/gensyn-ai/rl-swarm.git
cd rl-swarm
```
3️⃣ Setup Virtual Environment & Run the Node
```
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

4️⃣ Follow Prompts

- Push models to Hugging Face? → N
- Enter model name or press Enter for default → just press Enter
- Participate in AI Prediction Market? → Y

✅ Done! Your node is now running successfully.

- CTRL A + D 

## Access Web UI (http://localhost:3000)

If running on VPS, use Cloudflared to access the dashboard from your browser. 
## Open another tab on your VPS
```
sudo apt install -y ufw
sudo ufw allow 22
sudo ufw allow 3000/tcp
sudo ufw enable
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
sudo dpkg -i cloudflared-linux-amd64.deb
cloudflared tunnel --url http://localhost:3000
```
- Then open the HTTPS link shown in your terminal.
<img width="1754" height="226" alt="image" src="https://github.com/user-attachments/assets/2ae7c569-7f40-4db3-89f4-02562d076dca" />

- Sign up gensyn acc.
- Done ✅



💾 Backup Your Node Key open another vps tab

After first successful run, backup your key file:
```
cp ~/rl-swarm/swarm.pem ~/swarm.pem.backup
```

# FAQ & Troubleshoot

⚙️ Fix “Terminated” / “Killed” Errors

- If your process stops with Killed or Terminated:
```
git stash
git switch main
git reset --hard
git clean -fd
git pull origin main
deactivate
rm -rf .venv && python3 -m venv .venv && source .venv/bin/activate
./run_rl_swarm.sh
```
- still using Node.js v18, even though you’ve already updated to v20.
<img width="1194" height="872" alt="image" src="https://github.com/user-attachments/assets/5e6b09d9-0344-4aab-9b04-3e3abb02f36c" />

✅ Solution (Fix Node Version to 20+)
```
# 1️⃣ Remove old Node.js version
sudo apt remove -y nodejs

# 2️⃣ Install Node.js 20 again
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# 3️⃣ Verify correct version
node -v
```

Output should be: 
```v20.18.0  (or higher)```



🧩How To Grab Your Gswarm Role:
- You can do this process both in ubuntu or codespace

</div>


## 1. Install Go

### Linux/Wsl

```
wget https://go.dev/dl/go1.24.0.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.24.0.linux-amd64.tar.gz
```

```
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
echo 'export GOPATH=$HOME/go' >> ~/.bashrc
echo 'export PATH=$PATH:$GOPATH/bin' >> ~/.bashrc
source ~/.bashrc
```

* >Verify installation

```
go version
```

## 2. Telegram Bot Set-Up 🤖

> To receive notifications via Telegram, you need to set up a Telegram bot and connect it to your account:


### 2.1 Create a Telegram Bot:

* Go To  https://t.me/BotFather

* Send `/newbot` and follow the instructions:

* It will Ask You to enter the Name & username of the Bot: 

* Now it will send the Token. Look Like this: `84100000:AAGITsRXgxxxxNuP56-xxxxxxxxxxxxxxx` dont share with anyone:


### 2.2 Get Your Chat ID:

* head to your bot which was created and send message:

* Visit: https://api.telegram.org/botYOUR_BOT_TOKEN/getUpdates 

* Dont Forget to replace `YOUR_BOT_TOKEN` with your: which we create in above step:

* You will see your `Id` here : Save it: 

* >Note: If you get an empty result {"ok":true,"result":[]}, you may need to send a message to your bot first, then refresh the URL.

<img width="2196" height="253" alt="image" src="https://github.com/user-attachments/assets/3d399c11-6c10-4d80-a880-a78fd2050ebf" />




## 3. Installation & Configure GSwarm

### 1. Installation

```
go install github.com/Deep-Commit/gswarm/cmd/gswarm@latest
```

* >Verify installation:

```
gswarm --version
```



### 2. Configure GSwarm:

* > We will config our Gensyn Node and telegram bot here: Will Add `bot token`, `chat ID`, and `EOA address`

```
gswarm
```

* Enter Your BotToken from : 2.1 Create a Telegram Bot:

* Enter Your ChainId From : 2.2 Get Your Chat ID:

* Enter Your EOA address From: [Gensyn Dashboard](https://dashboard.gensyn.ai/)      --Login with your gensyn Mail:


## 4. 🔗 Linking Discord & Telegram:


### 1. Get the verification code From Discord

* In Gensyn Dc go to `swarm-link channel` 

* Enter `/link-telegram` 

* You will get your code from here:


### 2. Verify the code in Telegram Bot

* Go to Your bot which you creat:

* type `/verify {code}` , Replace `code` with your actual one: which u got from DC:

* After verify your code You will automatically get your Role:

<img width="1596" height="797" alt="image" src="https://github.com/user-attachments/assets/050b4be4-7175-461c-9133-c88e17d12663" />



✔️✔️✔️Done:


# 🧩 Gensyn AI Block Assist Role Guide

This guide explains how to deploy the **Gensyn Block Assist app** using **Octa.Space VPS** and link it to your **Hugging Face** and **Discord** for verification and rewards.

---

## ⚙️ Requirements

| Resource | Minimum | Recommended |
|-----------|----------|-------------|
| GPU       | 1× RTX 3090 24 GB | or any similar GPU |
| CPU       | 4 cores | 6+ cores |
| RAM       | 8 GB | 16 GB |
| Storage   | 50 GB | 100 GB |
| Token     | 1 OCTA (~$0.30) | For 1-hour VPS rental |

---

## 🧱 Step 1: Create Octa.Space Account

1. Visit 👉 [https://marketplace.octa.space](https://marketplace.octa.space)
2. **Create an account** and **copy your Octa wallet address.**
3. **Deposit at least 1 OCTA** token to your Octa wallet address.  
   You can buy and send OCTA using any exchange like **MEXC**.

---

## 🤖 Step 2: Create Hugging Face Token

1. Visit 👉 [https://huggingface.co](https://huggingface.co)
2. Sign up or log in.
3. Go to your **Profile → Settings → Access Tokens.**
4. Click **“New Token”**  
   - **Name:** `BlockAssist`  
   - **Role:** `Write` (important)  
5. Click **Create**.
6. **Copy and save the token immediately.**  
   ⚠️ You won’t see it again. If lost, delete and make a new one.

---

## 🚀 Step 3: Deploy Gensyn Block Assist on Octa.Space

1. Go back to 👉 [https://marketplace.octa.space](https://marketplace.octa.space)
2. In the search bar, type **“Gensyn”** and select **“Gensyn Block Assist.”**
3. Click **“VPS”** and select:
   - **Type:** `1x RTX 3090 24 GB` *(or any available GPU)*
   - **Duration:** `1 hour`
   - **Cost:** ≈ `0.3 OCTA ($0.10)`
4. Click **Configure.**

---

## 🔑 Step 4: Configure the Block Assist App

In the configuration section:
- You will see a field labeled **“value cannot be empty.”**
- Paste the following: HF_TOKEN

<img width="1280" height="563" alt="image" src="https://github.com/user-attachments/assets/45401b24-927f-4115-861d-c53be9787a97" />


- In the **“value” box**, paste your **Hugging Face token** you created earlier.

<img width="1280" height="692" alt="image" src="https://github.com/user-attachments/assets/c9fa3704-31e9-4fc5-99bb-6334473f0c8b" />

- Click **Deploy.**

---

## ⏳ Step 5: Wait for VPS to Launch

- Wait **1–2 minutes** after deployment.
- Then click your deployed VPS → click the **HTTPS link**.  
It will open the **Gensyn Block Assist** interface.  
(It might take another 1–2 minutes to fully load.)

---

## 🎮 Step 6: Play Minecraft (Recording Session)
<img width="680" height="367" alt="image" src="https://github.com/user-attachments/assets/d9d72fd4-c1f9-4a88-a18d-c7420d249322" />

Once the app loads:

1. Log in — two **Minecraft** windows will open automatically.
2. Wait for the **command window** to appear.
3. Press **ENTER** — this starts the **recording timer**.
4. Go to the **first Minecraft window** and play for **1–2 minutes**.
5. After playing, return to the command window.
6. Press **ENTER** three (3) times.  
 → All windows will close automatically.


---

## 💾 Step 7: Verify Your Hugging Face Model

1. Go back to 👉 [https://huggingface.co](https://huggingface.co)
2. Open your **Profile** page.  
 You’ll now see a new **BlockAssist model** listed.
3. Click it and **copy the full browser URL** (e.g. `https://huggingface.co/username/blockassist`).

---

## 💬 Step 8: Verify in Discord

> ⚠️ You **must already have the Swarm role** from the RL-Swarm setup before continuing.

### 1️⃣ Verify Hugging Face Token
- Go to the **#links-access** channel in Discord.
- Type: /verify-huggingface
- When asked, paste your **Hugging Face token**.

### 2️⃣ Verify Block Assist
- Go to the **#the-swarm** channel.
- Type: /verify-block
- When asked, paste your **Hugging Face BlockAssist model link**.

✅ Within a minute, you’ll receive your **Block Assist role**.

You should now have:
✅ Swarm Role
✅ Block Role
✅ 1-Day Gensyn Node Uptime via Octa VPS

---

## 🧹 Step 9: Stop the VPS (After Role is Granted)

Once your Discord role is confirmed:
- Go to your Octa dashboard.
- Click **“Stop Session”** for the VPS you deployed.  
  → No need to keep your laptop or VPS running afterward.

---

## ⚠️ Troubleshooting

| Issue | Solution |
|--------|-----------|
| ❌ VPS stuck on “loading” | Wait 2–3 minutes, then refresh. If still stuck after 5 minutes, stop and redeploy. |
| ⚠️ Terminated / Killed | Your VPS ran out of memory (OOM). Use a higher-RAM plan (16 GB+). |
| 💀 No Hugging Face model appears | Wait 2–5 minutes, then refresh your Hugging Face profile. |
| 🕹️ Minecraft windows won’t open | Make sure GPU VPS was used (RTX 3090 or similar). |

---

## 🎯 Done!

You have now successfully:
- ✅ Verified Swarm node  
- ✅ Earned Block Assist role  
- ✅ Linked Hugging Face + Discord  
- ✅ Completed 1-day Gensyn uptime via Octa.Space  

Keep exploring to unlock more Gensyn ecosystem rewards 🚀

---






















































