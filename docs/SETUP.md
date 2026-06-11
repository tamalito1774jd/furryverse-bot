# Setup Guide - FurryVerse Bot

Complete guide to install and configure FurryVerse Bot.

## 📋 Requirements

### Minimum
- **Node.js**: v18.0.0 or higher
- **npm**: v9.0.0 or higher
- **RAM**: 2GB minimum
- **Disk**: 5GB minimum
- **OS**: Linux, macOS, or Windows

### Recommended
- **Node.js**: v20.0.0 or higher
- **RAM**: 4GB or higher
- **Disk**: 20GB SSD
- **OS**: Ubuntu 20.04 LTS or higher

### Services Required
- **Discord Server**: For testing the bot
- **MongoDB**: For data storage
- **PostgreSQL**: For logs and stats
- **Redis**: For caching

## 🚀 Quick Start

### 1. Clone Repository
```bash
git clone https://github.com/tamalito1774jd/furryverse-bot.git
cd furryverse-bot
```

### 2. Create Environment File
```bash
cp .env.example .env
```

### 3. Configure Environment
Edit `.env` with your credentials:

```env
# Discord Bot
DISCORD_TOKEN=your_bot_token_here
DISCORD_CLIENT_ID=your_client_id
DISCORD_CLIENT_SECRET=your_client_secret

# Databases
MONGODB_URI=mongodb://localhost:27017/furryverse
POSTGRESQL_URI=postgresql://user:password@localhost:5432/furryverse
REDIS_URI=redis://localhost:6379

# API
API_PORT=3000
NODE_ENV=development
```

### 4. Start with Docker
```bash
docker-compose up -d
```

### 5. Verify Installation
```bash
# Check services
docker-compose ps

# View logs
docker-compose logs -f bot
```

## 📖 Detailed Installation

### Step 1: Install Node.js

**Ubuntu/Debian:**
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

**macOS:**
```bash
brew install node
```

**Windows:**
Download from [nodejs.org](https://nodejs.org/)

### Step 2: Create Discord Bot

1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Click "New Application"
3. Set name: "FurryVerse Bot"
4. Go to "Bot" section
5. Click "Add Bot"
6. Copy token → paste in `.env` as `DISCORD_TOKEN`
7. Enable required intents:
   - Server Members Intent
   - Message Content Intent
   - Guild Messages Intent

### Step 3: Install Docker

**Ubuntu:**
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
```

**macOS:**
Download [Docker Desktop](https://www.docker.com/products/docker-desktop)

**Windows:**
Download [Docker Desktop](https://www.docker.com/products/docker-desktop)

### Step 4: Setup Services

```bash
# Start databases and Redis
docker-compose up -d mongodb postgresql redis

# Wait for services to be healthy
sleep 10

# View service status
docker-compose logs mongodb postgresql redis
```

### Step 5: Install Dependencies

```bash
# Root dependencies
npm install

# Individual services
cd bot && npm install
cd ../backend && npm install
cd ../dashboard && npm install
cd ..
```

### Step 6: Build Services

```bash
npm run build
```

### Step 7: Start Services

```bash
# Development
npm run dev

# Production
docker-compose up -d
```

## 🔧 Configuration Details

### Discord Bot Configuration

**In Discord Developer Portal:**

1. **OAuth2 Settings**:
   - Go to OAuth2 → URL Generator
   - Select scopes: `bot`
   - Select permissions:
     - Manage Messages
     - Ban Members
     - Kick Members
     - Moderate Members
     - Manage Roles
     - Manage Channels
     - Send Messages
     - Embed Links
     - Attach Files
     - Read Message History
     - Mention @everyone
     - Use Application Commands

2. **Invite Bot**:
   - Copy generated URL
   - Paste in browser
   - Select server
   - Authorize

### Database Configuration

**MongoDB:**
```bash
# Local MongoDB
mongosh

# Connect to furryverse database
use furryverse

# Create indexes
db.users.createIndex({ discordId: 1 })
db.servers.createIndex({ discordId: 1 })
```

**PostgreSQL:**
```bash
# Connect to database
psql -U furryverse -d furryverse

# Run migrations
\q
npm run migrate
```

### Redis Configuration

```bash
# Test connection
redis-cli ping
# Should return: PONG
```

## ✅ Verification Checklist

After setup, verify:

- [ ] Node.js v18+: `node --version`
- [ ] npm v9+: `npm --version`
- [ ] Docker running: `docker ps`
- [ ] MongoDB running: `docker-compose logs mongodb`
- [ ] PostgreSQL running: `docker-compose logs postgresql`
- [ ] Redis running: `docker-compose logs redis`
- [ ] Bot online: Check Discord server
- [ ] API running: `curl http://localhost:3000/health`
- [ ] Dashboard accessible: `http://localhost:3001`

## 🐛 Common Issues

### Bot doesn't respond
```bash
# Check if bot is online
docker-compose logs bot

# Verify Discord token
grep DISCORD_TOKEN .env

# Check Discord intents are enabled
```

### Database connection error
```bash
# Check MongoDB status
docker-compose logs mongodb

# Check connection string
grep MONGODB_URI .env

# Test connection
mongosh $MONGODB_URI
```

### Port already in use
```bash
# Find process using port
lsof -i :3000

# Change port in .env
API_PORT=3001
```

### Permission denied
```bash
# Make scripts executable
chmod +x scripts/*.sh

# Add user to docker group
sudo usermod -aG docker $USER
newgrp docker
```

## 📞 Need Help?

- 📧 Email: support@furryverse-bot.com
- 💬 Discord: [Support Server](https://discord.gg/furryverse)
- 🐛 Issues: [GitHub Issues](https://github.com/tamalito1774jd/furryverse-bot/issues)

## 🔗 Useful Links

- [Discord.js Documentation](https://discord.js.org/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Next.js Documentation](https://nextjs.org/docs)
- [Docker Documentation](https://docs.docker.com/)

---

**Last Updated**: 2024-06-11  
**Status**: ✅ Complete
