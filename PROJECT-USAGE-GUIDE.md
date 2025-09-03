# 📚 AI Agent Framework - Installation & Usage Guide

**Current Claude Code**: v1.0.102  
**Repository**: https://github.com/mdastpak/agents  
**Upstream**: https://github.com/contains-studio/agents  

---

## 🎯 **What This Is**

The **AI Agent Framework** is a collection of **54 specialized AI agents** that work with **Claude Code CLI** to provide expert-level software development assistance. Each agent acts as a domain specialist.

### **What You Get:**
- **54 Expert Agents** across all development domains
- **Ready-to-use commands** for Claude Code CLI
- **Multi-agent coordination** for complex projects
- **Cross-platform support** (macOS, Linux, Windows)
- **Open source** with active development

---

## 🚀 **Step-by-Step Installation**

### **System Requirements Check**
```bash
# Check your OS
uname -a
# Expected: Darwin [hostname] 25.0.0 (macOS) or Linux/Windows equivalent

# Check Node.js (required v16+)
node --version
# Expected: v22.17.1 or higher

# Check if Claude is already installed
which claude
# Shows: /usr/local/bin/claude or /Users/[user]/.claude/local/claude

whereis claude  
# Shows: claude: /usr/local/bin/claude

# Check Claude version
claude --version
# Expected: 1.0.102 (Claude Code) or newer
```

### **Step 1: Install Claude Code (Platform-Specific)**

#### **macOS (Darwin 25.0.0+)**
```bash
# Claude Code is typically installed via direct download, not npm
# Download from: https://claude.ai/code
# Or if available via homebrew:
brew install claude-code  # (if available)

# Verify installation location
ls -la ~/.claude/local/
# Should show claude executable

# Add to PATH if needed (add to ~/.zshrc or ~/.bash_profile)
echo 'export PATH="$HOME/.claude/local:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

#### **Linux (Ubuntu/Debian)**
```bash
# Download and install Claude Code
wget https://claude.ai/code/download/linux
sudo dpkg -i claude-code.deb

# Or via snap (if available)
sudo snap install claude-code

# Verify
which claude
```

#### **Windows (PowerShell)**
```powershell
# Download Claude Code installer from https://claude.ai/code
# Run installer as administrator
# Or via chocolatey (if available)
choco install claude-code

# Verify in Command Prompt
claude --version
```

### **Step 2: Clone the Repository**
```bash
# Clone the actual working repository
git clone https://github.com/mdastpak/agents.git ai-agent-framework
cd ai-agent-framework

# Verify you have all the agents
find . -name "*.md" -path "*/backend/*" -o -path "*/blockchain/*" -o -path "*/meta-agents/*" | wc -l
# Should show: 54+ files

# Check current location
pwd
# Should show: /Users/[user]/[path]/ai-agent-framework
```

### **Alternative: Download ZIP**
```bash
# If you can't use git
wget https://github.com/mdastpak/agents/archive/refs/heads/agent-enhancement-v2.1.zip
unzip agent-enhancement-v2.1.zip
cd agents-agent-enhancement-v2.1/
```

### **Step 3: Verify Project Structure & Fix Path Issues**
```bash
# You should be in the project directory
pwd
# Output: /Users/[user]/[path]/ai-agent-framework
# IMPORTANT: Note the EXACT path - you'll need it for .claude/settings.local.json

# Check that .claude directory exists (it should already be there)
ls -la .claude/
# Should show: settings.local.json and other config files

# CRITICAL: Fix common path typo in settings
cat .claude/settings.local.json
# Look for "additionalDirectories" - verify path matches your pwd output
# Common error: "/Users/dmp/..." should be "/Users/dpm/..."

# If path is wrong, edit the file:
# Replace incorrect path with your actual pwd output

# Verify agent categories are present
ls -1 | grep -E '^(backend|blockchain|frontend|meta-agents)'
# Should show: backend, blockchain, frontend, meta-agents, etc.

# Count total agent files
find . -name "*.md" -path "./backend/*" -o -path "./blockchain/*" -o -path "./frontend/*" -o -path "./mobile/*" -o -path "./devops/*" -o -path "./qa/*" -o -path "./content/*" -o -path "./marketing/*" -o -path "./operations/*" -o -path "./product/*" -o -path "./project-management/*" -o -path "./meta-agents/*" | wc -l
# Should output: 54
```

### **Step 4: Test Claude Code Works**
```bash
# Start Claude in the project directory (IMPORTANT: must be in project root)
cd /path/to/ai-agent-framework  # Replace with your actual path
claude

# Test basic functionality first
# In Claude prompt, type:
hello

# Test file reading capability
cat AGENT-DEPLOYMENT-CATALOG.md
```

### **Step 5: Test Your First Agent**
```bash
# In Claude Code CLI, use these EXACT commands:

# Test Meta-Agent Integration System
claude "Act as the Meta-Agent Integration System from /meta-agents/meta-agent-integration-system.md and introduce the AI Agent Framework capabilities with a brief overview of the 54 agents available."

# Test Backend Architect
claude "Act as the Backend Architect from /backend/backend-architect.md and design a high-level architecture for a web application backend system."

# Test Blockchain Architect
claude "Act as the Blockchain Architect from /blockchain/blockchain-architect.md and design a basic wallet system architecture."
```

### **Step 6: Restart Claude (When/How)**
```bash
# Exit Claude Code session
Ctrl+C  # or Ctrl+D on some systems

# Restart in project directory
cd /Users/[user]/[path]/ai-agent-framework  # Use your actual path
claude

# Alternative: Use multiple terminal sessions
# Terminal 1: Keep Claude running
# Terminal 2: Edit files, run git commands, etc.
```

---

## 📁 **Project Structure**

```bash
ai-agent-framework/
├── .claude/                          # Claude Code configuration
│   └── settings.local.json          # Local permissions
├── backend/                          # Backend development (4 agents)
│   ├── admin-panel-backend.md
│   ├── backend-architect.md
│   ├── strapi-integrator.md
│   └── user-panel-backend.md
├── blockchain/                       # Blockchain & crypto (4 agents)
│   ├── blockchain-architect.md
│   ├── defi-integrator.md
│   ├── security-auditor.md
│   └── trading-engine.md
├── content/                         # Content management (4 agents)
├── devops/                          # DevOps & infrastructure (3 agents)
├── frontend/                        # Frontend development (4 agents)
├── marketing/                       # Marketing (1 agent)
├── meta-agents/                     # Meta-orchestration (10 agents)
│   └── meta-agent-integration-system.md  # Master orchestrator
├── mobile/                          # Mobile development (3 agents)
├── operations/                      # Operations management (8 agents)
├── product/                         # Product management (5 agents)
├── project-management/              # Project management (3 agents)
└── qa/                             # Quality assurance (2 agents)

# Verify structure:
find . -name "*.md" -path "./*/\*" | wc -l  # Should show: 54
ls -1 | grep -E '^(backend|blockchain|frontend|meta-agents)$'
```

---

## 🔧 **Using the Agents**

### **Basic Agent Commands**
```bash
# IMPORTANT: Run these commands inside Claude Code CLI

# General format:
claude "Act as the [Agent Name] from /[category]/[agent-file].md and [your request]"

# Start with the master orchestrator:
claude "Act as the Meta-Agent Integration System from /meta-agents/meta-agent-integration-system.md and introduce the framework capabilities"

# Backend development:
claude "Act as the Backend Architect from /backend/backend-architect.md and design a microservices architecture for an e-commerce platform"

# Frontend development:
claude "Act as the User Panel Frontend from /frontend/user-panel-frontend.md and create a responsive dashboard design"

# Mobile development:
claude "Act as the iOS Specialist from /mobile/ios-specialist.md and outline the architecture for a native iOS app"

# DevOps and infrastructure:
claude "Act as the DevOps Automator from /devops/devops-automator.md and set up a CI/CD pipeline"

# Content and marketing:
claude "Act as the Content Strategist from /content/content-strategist.md and create a content plan for a tech startup"
```

### **Multi-Agent Coordination**
```bash
# Use the Meta-Agent Integration System for coordination:
claude "Act as the Meta-Agent Integration System and coordinate a full-stack web application project using the appropriate specialized agents"

# Or manually coordinate specific agents:
claude "I need the Backend Architect and DevOps Automator to work together on designing a scalable deployment strategy"
```

### **Common Use Cases**
```bash
# Web Application Development
claude "Act as the Backend Architect from /backend/backend-architect.md and design a REST API for a social media platform"
claude "Act as the Site Frontend from /frontend/site-frontend.md and create a modern landing page design"
claude "Act as the DevOps Automator from /devops/devops-automator.md and set up automated deployment"

# Mobile App Project
claude "Act as the iOS Specialist from /mobile/ios-specialist.md and plan a native iOS app architecture"
claude "Act as the Android Specialist from /mobile/android-specialist.md and create an Android development roadmap"
claude "Act as the Mobile Security from /mobile/mobile-security.md and implement security best practices"

# Content and Marketing
claude "Act as the Content Strategist from /content/content-strategist.md and develop a content marketing plan"
claude "Act as the SEO Specialist from /marketing/seo-specialist.md and optimize website content for search engines"
```

---

## 🔄 **Common Workflows**

### **Starting a New Project**
1. Clone/copy the agent framework
2. Start Claude Code in the project directory
3. Begin with Meta-Agent Integration System for project overview
4. Deploy relevant specialized agents for your domain
5. Test individual agents, then try coordination

### **Real-World Troubleshooting**

#### **"Path was not found" Error (MOST COMMON)**
```bash
# Error: "Path /Users/dmp/Downloads/Projects/dmp/agents was not found."
# When your actual path is: /Users/dpm/Downloads/Projects/dpm/agents

# Step 1: Find your actual path
pwd
# Copy the exact output

# Step 2: Check Claude settings
cat .claude/settings.local.json
# Look for typos in "additionalDirectories"

# Step 3: Fix the path typo
# Edit .claude/settings.local.json
# Replace wrong path with correct one from pwd

# Step 4: Restart Claude
# Exit (Ctrl+C) and restart: claude
```

#### **Agent Not Responding**
```bash
# 1. Verify you're in the correct directory
pwd
# Should show: /Users/[user]/[path]/ai-agent-framework

# 2. Check for path typo in Claude settings (MOST COMMON ISSUE)
cat .claude/settings.local.json
# Look for "additionalDirectories" - must match your pwd exactly
# Example error: "/Users/dmp/..." when actual is "/Users/dpm/..."

# 3. Check if agent file exists
ls -la backend/backend-architect.md
# Should show file with size > 0 bytes

# 4. Verify Claude can read files (in Claude CLI):
cat backend/backend-architect.md | head -10

# 5. Test with minimal command first
claude "hello"
claude "what is 2+2?"
```

#### **Path Errors**
```bash
# Common error: "Path not found"
# Fix: Use exact paths from project structure

# WRONG:
claude "Act as Backend Architect and design system"

# RIGHT:
claude "Act as the Backend Architect from /backend/backend-architect.md and design a system architecture"

# Verify paths:
find . -name "backend-architect.md"
# Output: ./backend/backend-architect.md
```

#### **Restarting Claude Code (Platform-Specific)**
```bash
# macOS/Linux:
Ctrl+C    # Exit Claude session
cd /Users/[user]/[path]/ai-agent-framework  # Navigate to project
claude    # Start new session

# Windows (Command Prompt):
Ctrl+C    # Exit Claude session
cd C:\Users\[user]\[path]\ai-agent-framework
claude.exe

# Alternative: Kill process (if hung)
# macOS/Linux:
ps aux | grep claude
kill [process_id]

# Windows:
tasklist | findstr claude
taskkill /PID [process_id] /F
```

---

## 📤 **Publishing Your Project**

### **Prepare for Publishing**

1. **Clean Up Project**
```bash
# Remove sensitive information
rm -f .claude/settings.local.json  # Contains local paths
git clean -fd  # Remove untracked files

# Create generic settings template
cp .claude/settings.local.json .claude/settings.template.json
# Edit template to remove personal paths
```

2. **Update Documentation**
```bash
# Update README with your specific use case
# Update ROADMAP with your plans
# Ensure all agent files are present and tested
```

3. **Create Release**
```bash
# Tag your version
git tag -a v1.0.0 -m "Initial release of customized AI Agent Framework"
git push origin v1.0.0
```

### **GitHub Repository (Actual Working Example)**
```bash
# This project's actual GitHub setup:
git remote -v
# Shows:
# origin    https://github.com/mdastpak/agents.git (fetch)
# origin    https://github.com/mdastpak/agents.git (push)
# upstream  https://github.com/contains-studio/agents.git (fetch)
# upstream  https://github.com/contains-studio/agents.git (push)

# To fork/clone for your own use:
1. Fork https://github.com/mdastpak/agents on GitHub
2. Clone your fork:
git clone https://github.com/[your-username]/agents.git my-agent-framework
cd my-agent-framework

# Set up your own repository:
git remote rename origin upstream
git remote add origin https://github.com/[your-username]/[your-repo-name].git
git push -u origin main

# Keep upstream for updates:
git fetch upstream
git merge upstream/main  # When you want updates
```

### **NPM Package** (Advanced)
```bash
# Create package.json
npm init

# Add to package.json:
{
  "name": "your-agent-framework",
  "version": "1.0.0",
  "description": "AI Agent Framework for Claude Code",
  "main": "index.js",
  "scripts": {
    "install": "npm install -g @anthropic/claude-code"
  },
  "files": [
    "backend/",
    "blockchain/",
    "frontend/",
    "meta-agents/",
    "*.md"
  ]
}

# Publish
npm publish
```

---

## 🆘 **Troubleshooting**

### **Common Issues**

| Problem | Real Solution |
|---------|---------------|
| Agent not responding | 1. `pwd` (check you're in project root)<br>2. `ls backend/backend-architect.md` (verify file exists)<br>3. Restart: `Ctrl+C`, then `claude` |
| "Path not found" error | Use absolute paths: `/backend/backend-architect.md`<br>Not relative: `backend-architect.md` |
| **"Path /Users/dmp/...was not found"** | **COMMON TYPO**: Check `.claude/settings.local.json`<br>Fix path typos (dmp→dpm, etc.)<br>Verify actual path with `pwd` |
| Permission errors | Check `.claude/settings.local.json` has correct paths<br>Match your actual directory structure |
| Claude Code not found | **Not installed via npm!**<br>Download from https://claude.ai/code<br>Install to `~/.claude/local/claude` |
| Multiple installations warning | Normal - you have local + global installs<br>Currently using: npm-local (1.0.102) |
| Coordination failures | Start with: `Meta-Agent Integration System`<br>Then individual agents |
| Commands time out | Use shorter, more specific requests<br>Break complex tasks into steps |

### **Debug Commands (Real System)**
```bash
# Check Claude Code installation and version
claude --version
# Expected: 1.0.102 (Claude Code) or newer

# Find Claude installation location
which claude
# Output: /usr/local/bin/claude or ~/.claude/local/claude

whereis claude
# Output: claude: /usr/local/bin/claude

# Check Node.js (required for some features)
node --version
# Expected: v22.17.1 or newer

# Verify project structure
ls -la backend/ | head -5
# Should show: admin-panel-backend.md, backend-architect.md, etc.

ls -la meta-agents/ | head -5  
# Should show: meta-agent-integration-system.md, etc.

# Count agent files
find . -name "*.md" -path "./*/\*" | wc -l
# Should show: 54+ files

# Test Claude Code basic functionality
# Run inside Claude CLI:
hello
what is the current directory?
ls -la
```

---

## 📞 **Support & Resources**

### **Getting Help**
```bash
# Claude Code help
claude --help
claude --version

# Project-specific help
cat AGENT-DEPLOYMENT-CATALOG.md | head -50  # Agent reference

# GitHub Issues (actual repository)
# https://github.com/mdastpak/agents/issues
# https://github.com/contains-studio/agents/issues (upstream)
```

### **Key Documentation Files**
1. **`PROJECT-USAGE-GUIDE.md`** - This installation and usage guide
2. **`AGENT-DEPLOYMENT-CATALOG.md`** - Complete list of all 54 agents
3. **`README.md`** - Project overview and quick start
4. **`ROADMAP.md`** - Development plans and future features

### **Quick Success Test**
```bash
# Run this sequence to verify everything works:

# 1. Check location and structure
pwd && ls -la | grep -E '^d.*(agents|backend)'

# 2. Start Claude and test basic agent
claude "Act as the Meta-Agent Integration System from /meta-agents/meta-agent-integration-system.md and briefly explain what this AI Agent Framework can do."

# 3. Test specialized agent
claude "Act as the Backend Architect from /backend/backend-architect.md and suggest a basic 3-tier architecture."

# If both work: ✅ SUCCESS - Framework is operational!
# If either fails: Check troubleshooting section above
```

---

## 🚀 **You're Ready!**

**What you now have:**
- ✅ **54 Expert AI Agents** across all development domains
- ✅ **Working commands** with real examples  
- ✅ **Multi-agent coordination** capabilities
- ✅ **Comprehensive troubleshooting** guide
- ✅ **Open source framework** ready for customization

**Next steps:**
1. Run the "Quick Success Test" to verify installation
2. Start with simple single-agent commands
3. Try multi-agent coordination for complex projects
4. Customize agents for your specific needs
5. Contribute improvements back to the community

**Happy coding with 54 AI Agent specialists!** 🤖✨🚀