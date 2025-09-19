# Sentient ROMA - Installation Guide


Why Did I Prepare This Guide?
As you may know, ROMA is an open-source meta-agent framework developed by the Sentient team. Its purpose is to enable multiple lightweight agents to work together to solve high-performance, complex tasks. The team prepared a GitHub guide for installing ROMA, and it reached the #1 spot on GitHub trends. However, there isn't a guide that everyone can easily follow. I prepared this guide so that everyone can install and experience ROMA. By following the simple steps in this guide, you can get ROMA running on your computer and witness firsthand how it solves complex tasks. Let's get started...




# 1-UBUNTU INSTALLATION
Search for "Ubuntu" in the Microsoft Store apps and install it. After completion, a terminal screen will open and it will perform an automatic update.
.
.
<img width="1873" height="934" alt="ubuntu mic skur" src="https://github.com/user-attachments/assets/7dc0347c-05b1-417e-a596-45c996f81e22" />


# 2-OPENROUTER ACCOUNT CREATION

Go to https://openrouter.ai/ and sign in with your Google account. Click on the Settings (gear icon) in the top right corner, then go to Keys. Click on "API Keys", then click "Create API Key". On the screen that appears, give it a name in the "Name" field and click the "Create" button to generate your API key. Note down your API key (starts with sk-). Be careful, as you cannot see your API key again after closing the screen.

<img width="1860" height="913" alt="openrouter keys" src="https://github.com/user-attachments/assets/ea75ee63-90a6-4721-af76-fc4bf0ecb121" />
<img width="1813" height="745" alt="openrotuer sk key" src="https://github.com/user-attachments/assets/0df772f4-4588-4cbc-9596-5c989bad222a" />

# 3-DOCKER DESKTOP INSTALLATION
Go to https://www.docker.com/products/docker-desktop/. Download Docker for Windows from the "Download Docker Desktop" section and install it on your computer. After restarting, run Docker Desktop from your desktop. Click "Continue without signing in". After the installation is complete, you should see "Docker Desktop Running" in the bottom right corner of your desktop. If it gives an error, close and reopen it; it should work after performing an update.





<img width="1885" height="763" alt="docker" src="https://github.com/user-attachments/assets/76935b53-4bae-4c6e-bf34-fe689b12e92f" />
<img width="707" height="401" alt="docker setup" src="https://github.com/user-attachments/assets/6ddb4223-6dfd-4983-8fb8-5ad2602e1b98" />


Then, click the settings (gear) icon in the top right corner. Under the Resources section, go to WSL Integration, enable Ubuntu, and click Restart & Apply to activate Ubuntu. If Ubuntu does not appear in the WSL Integration section; search for "Terminal" or "Windows PowerShell" in your computer's search bar, open the command prompt, and type the following commands in order. It will ask you to create a username and password. Define your username and password.

```Bash
wsl --install -d Ubuntu-22.04
wsl -s Ubuntu-22.04

```

<img width="871" height="452" alt="wal" src="https://github.com/user-attachments/assets/009707ea-7635-4164-8f75-1b08fa4d00fd" />

<img width="1890" height="966" alt="docker ubuntu aktif" src="https://github.com/user-attachments/assets/7fcf0b2e-c240-491c-85ba-f41464c1cd60" />


Now, search for "Ubuntu 22.04.05" on your computer and run the Ubuntu program we installed earlier. A terminal command window will open; it may ask you to set a username and password again. Enter any username and password. From now on, we will run all commands using the Ubuntu terminal.


<img width="947" height="396" alt="ubuntu kullanıc paralo" src="https://github.com/user-attachments/assets/e04fb3a3-4b99-483d-a5b3-80d5c9811cb0" />

Next, copy and paste the following codes one by one into the terminal line. If it asks for a password, enter the password you just set.

```Bash
sudo apt update && sudo apt upgrade -y
sudo apt install git docker.io docker-compose -y
```

<img width="945" height="491" alt="güncelleme ubuntu" src="https://github.com/user-attachments/assets/8a180d7d-253f-480a-92a9-f89b2b1a922e" />


Then, type the following commands in order into the terminal screen. The installation takes about 10 minutes; wait without closing the screen.

```Bash
git clone https://github.com/sentient-agi/ROMA.git
cd ROMA

./setup.sh --docker

```


<img width="946" height="493" alt="git roma1" src="https://github.com/user-attachments/assets/486f425e-134f-415e-b50d-f17ffa39a08b" />

<img width="947" height="491" alt="roma yüklendi" src="https://github.com/user-attachments/assets/cc0387b4-855f-42ca-a66e-c90df24a1f64" />

After the installation is complete, type the following codes in order into the terminal screen. 


```Bash
cd
cd ROMA
sed -i 's/api_key: "your-openrouter-key"/api_key: "${OPENROUTER_API_KEY}"/' sentient.yaml
```

<img width="950" height="383" alt="sentient yaml2" src="https://github.com/user-attachments/assets/9ee330f1-6c41-4c1e-b48b-9f8137dfc6a4" />


Now, let's write our API key. We obtained our API key from Openrouter above. Now, modify the part that says sk_write_your_api_key (write your sk- starting api key here) below by writing your own API key (starting with sk-). After writing your API key, copy the command and paste it into the terminal.

```Bash
cd
cd ROMA
sed -i 's/OPENROUTER_API_KEY=your_openrouter_key_here/OPENROUTER_API_KEY=sk_write_your_api_key/' .env

```
<img width="1900" height="666" alt="api keyi yaz tek komut" src="https://github.com/user-attachments/assets/424a2c7d-ad3a-4dd5-8b1e-369d5ecc1f95" />

Now, let's move on to editing the model ID. Paste the following commands into the terminal in order.


```Bash
cd
cd ~/ROMA/src/sentientresearchagent/hierarchical_agent_framework/agent_configs
sed -i 's/model_id:.*".*"/model_id: "openrouter\/deepseek\/deepseek-chat-v3.1:free"/g' agents.yaml openrouter/deepseek/deepseek-chat-v3.1:free

```

<img width="952" height="356" alt="model id" src="https://github.com/user-attachments/assets/8cd4fbbf-a997-4184-ac86-7528d1f76c8e" />

Now we are ready to start ROMA. Type the following codes in order into the terminal screen. Wait for 2-3 minutes.

```Bash
cd
cd ROMA
cd docker
docker compose down
docker compose up -d

```

<img width="950" height="443" alt="docker restart" src="https://github.com/user-attachments/assets/a7377f73-043d-4524-b73c-e75ba458c903" />

To check if there are any errors in the installation, let's check the logs. Run the following command, still in the docker folder. If everything is okay, you should see a screen similar to the one below. You can then press Ctrl+C to exit.

```Bash
docker compose logs -f

```

<img width="951" height="503" alt="log kontrol" src="https://github.com/user-attachments/assets/d99af0ae-ae87-4170-a47d-8462d447b003" />


Now go to http://localhost:3000/ in your browser and start using ROMA...

<img width="949" height="470" alt="roma tamam" src="https://github.com/user-attachments/assets/e020ddc0-1c27-4aca-a1ed-ae4698a675f2" />
