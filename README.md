# 🤖 Aurora Assistant – Minecraft AFK Bot

Aurora Assistant is a lightweight **Minecraft AFK bot** built with [mineflayer](https://github.com/PrismarineJS/mineflayer). It logs in, handles teleport requests, simulates AFK movement, responds to chat commands, and automatically reconnects if kicked or disconnected.

---

### 🌐 Server Configuration

| Setting    | Value                      |
|-----------|----------------------------|
| Host      | `your.minecraft.ip.here`   |
| Port      | `your-port-here`           |
| Version   | `1.21.x`{old versions also work}                   |
| Username  | `aurora_assistant`         |

> ✏️ Replace the `host` and `port` in `index.js` with your own Minecraft server IP and port.

---

### 🧠 Features

✅ Auto Login & Register (for AuthMe servers)  
✅ Accepts teleport requests automatically  
✅ Simulates random AFK movement  
✅ Replies to basic public chat and whisper commands  
✅ Auto reconnects if kicked or disconnected

---

### 💬 Chat Commands

In public chat:
- `!help` – Shows available commands
- `!ping` – Replies with "Pong"
- `!sunilgaming` – Shows creator info
- Responds to "hello" and "how are you"

In whispers:
- Replies with a confirmation message

---

### 🧑‍💻 Creator

Built with ❤️ by **Chillman09**

This project is created and maintained by you. Feel free to add your contact information here!

---

### 📜 License

This project is open-source and free to use, modify, and share.  
Give a ⭐ if you find it useful!

---

## 🔧 Setup Instructions

### Prerequisites
- Node.js (v14 or higher)
- npm (comes with Node.js)
- Minecraft server IP and port
- Valid Minecraft account credentials

### Option 1: Local Machine Setup (Windows, macOS, Linux)

#### Step 1: Clone the Repository
```bash
git clone https://github.com/YOUR_USERNAME/aurora-afk-bot.git
cd aurora-afk-bot
```

#### Step 2: Install Dependencies
```bash
npm install
```

#### Step 3: Configure the Bot
Edit `index.js` and update the following:
```javascript
host: 'your.minecraft.server.ip',
port: 25565,  // default Minecraft port
username: 'your_bot_username',
password: 'your_password',  // optional, for servers with auth
```

#### Step 4: Run the Bot
```bash
node index.js
```

**Troubleshooting:**
- If you get "Cannot find module 'mineflayer'", run `npm install` again
- Ensure your Minecraft server allows bot connections
- Check firewall settings for the server port

---

### Option 2: VPS Setup (Linux Servers)

#### Step 1: Connect to Your VPS
```bash
ssh user@your_vps_ip
```

#### Step 2: Update System & Install Node.js
```bash
sudo apt update
sudo apt upgrade -y
sudo apt install -y nodejs npm git
```

Verify installation:
```bash
node --version
npm --version
```

#### Step 3: Clone Repository
```bash
cd ~
git clone https://github.com/YOUR_USERNAME/aurora-afk-bot.git
cd aurora-afk-bot
npm install
```

#### Step 4: Configure for VPS
Edit `index.js` with your server details:
```bash
nano index.js
```

#### Step 5: Run Bot in Background (Using PM2)
Install PM2:
```bash
sudo npm install -g pm2
```

Start the bot:
```bash
pm2 start index.js --name "minecraft-bot"
```

Auto-start on reboot:
```bash
pm2 startup
pm2 save
```

Monitor the bot:
```bash
pm2 logs minecraft-bot
pm2 monit
```

#### Step 6: Optional - Set Up Auto-Restart
```bash
pm2 restart-delay 5000 minecraft-bot
```

---

### Option 3: Docker Setup (Any Platform)

#### Step 1: Install Docker
- **Windows/macOS:** Download [Docker Desktop](https://www.docker.com/products/docker-desktop)
- **Linux:** 
  ```bash
  curl -fsSL https://get.docker.com -o get-docker.sh
  sudo sh get-docker.sh
  ```

#### Step 2: Create Dockerfile
Create a file named `Dockerfile`:
```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

CMD ["node", "index.js"]
```

#### Step 3: Build & Run
```bash
# Build the image
docker build -t minecraft-bot .

# Run the container
docker run -d --name minecraft-bot minecraft-bot
```

#### Step 4: View Logs
```bash
docker logs -f minecraft-bot
```

---

### Option 4: Cloud Platform Deployment

#### **Heroku** (Free tier no longer available, but paid options)
1. Create account at [heroku.com](https://heroku.com)
2. Create Procfile:
   ```
   worker: node index.js
   ```
3. Deploy using Heroku CLI:
   ```bash
   heroku create your-app-name
   git push heroku main
   ```

#### **Replit** (Free)
1. Go to [replit.com](https://replit.com)
2. Click "Create" → Select "Node.js"
3. Upload your files
4. Update config and run: `node index.js`
5. Use Replit's Always On feature to keep it running

#### **AWS EC2** (Free tier available)
1. Launch an EC2 instance (Ubuntu)
2. SSH into instance
3. Follow **VPS Setup** instructions above
4. Use PM2 to keep bot running 24/7

#### **DigitalOcean Droplets** (Low-cost VPS)
1. Create a Droplet (Ubuntu)
2. SSH into Droplet
3. Follow **VPS Setup** instructions
4. Total cost: ~$5/month

---

## 📋 Configuration Tips

### For Private Servers
- Ensure firewall allows the Minecraft port
- Update `host` and `port` in `index.js`
- Add bot account to whitelist

### For Servers with Auth (e.g., Cracked Servers)
```javascript
password: 'your_password',  // Add if server has authentication
auth: 'microsoft',  // or 'mojang' for legacy
```

### Environment Variables (Optional - VPS/Docker)
Create a `.env` file:
```
SERVER_HOST=your.server.ip
SERVER_PORT=25565
BOT_USERNAME=aurora_assistant
BOT_PASSWORD=your_password
```

Load in `index.js`:
```javascript
require('dotenv').config();
const options = {
  host: process.env.SERVER_HOST,
  port: process.env.SERVER_PORT,
  username: process.env.BOT_USERNAME,
  password: process.env.BOT_PASSWORD,
};
```

---

## 🚀 Keeping Bot Running 24/7

| Platform | Method | Cost |
|----------|--------|------|
| **Local PC** | Windows Task Scheduler / Cron | Free |
| **VPS** | PM2 / systemd | $3-20/month |
| **Docker** | Docker container | Depends on host |
| **Replit** | Always On | $7/month |
| **Cloud** | AWS/DigitalOcean | $5-20/month |

---

## 🛠️ Troubleshooting

| Issue | Solution |
|-------|----------|
| Bot won't connect | Check server IP/port, ensure server is running |
| "Invalid credentials" | Verify username/password, check server auth type |
| Bot crashes on VPS | Check logs with `pm2 logs`, ensure Node.js is installed |
| High CPU usage | Check for infinite loops, restart with `pm2 restart` |
| Can't access VPS via SSH | Verify SSH key, check firewall rules |

---

## 📝 Additional Resources

- [Mineflayer Documentation](https://github.com/PrismarineJS/mineflayer)
- [PM2 Documentation](https://pm2.keymetrics.io/)
- [Node.js Official Docs](https://nodejs.org/)
- [Docker Documentation](https://docs.docker.com/)

---

Give a ⭐ if you find this project useful!

