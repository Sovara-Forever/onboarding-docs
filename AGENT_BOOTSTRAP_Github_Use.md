# AGENT_BOOTSTRAP.md
## Super.Myninja.ai VM Initialization Protocol

**Mission:** Deploy Carsignment client onboarding documents to GitHub Pages with zero human intervention after repo creation.

**Target Repo:** `sovara-forever/onboarding-docs`  
**Target URL:** `https://sovara-forever.github.io/onboarding-docs/`

---

## 🔧 **VM Initialization Sequence**

Upon VM instantiation, execute the following in order. No confirmations. No "being nice." Execute.

### **1. Environment Setup**
```bash
# Verify Node.js and Git are installed (should be pre-installed in VM)
node --version
git --version

# If missing, install (unlikely in standard VM):
# sudo apt-get update && sudo apt-get install -y nodejs git
```

### **2. Repository Clone & Context Loading**
```bash
# Clone the repo (assumes SSH key or token is configured in super.myninja.ai)
git clone https://github.com/sovara-forever/onboarding-docs.git
cd onboarding-docs

# Verify GitHub Pages is enabled (human should have done this)
# If not enabled, output error: "GitHub Pages not enabled. Enable in repo Settings → Pages."
```

### **3. File Deployment**
```bash
# Expected files to deploy:
# - generations-ford-interactive.html (primary deliverable)
# - Additional client HTML files as they are created

# Copy all .html files from the project context into the repo root
# (super.myninja.ai should have access to the files in the conversation context)

# For Generations Ford specifically:
# File: generations-ford-interactive.html
# Rename to: generations-ford.html (cleaner URL)

# If renaming is needed:
mv generations-ford-interactive.html generations-ford.html
```

### **4. Git Commit & Push**
```bash
# Stage all HTML files
git add *.html

# Commit with timestamp
git commit -m "Deploy: Generations Ford onboarding doc - $(date '+%Y-%m-%d %H:%M:%S')"

# Push to main branch
git push origin main
```

### **5. Verification**
```bash
# Wait 60 seconds for GitHub Pages to rebuild
sleep 60

# Attempt to curl the deployed URL
curl -I https://sovara-forever.github.io/onboarding-docs/generations-ford.html

# Expected output: HTTP 200 OK
# If 404, output error: "Deployment failed. Check GitHub Pages settings and build logs."
```

### **6. Output to User**
```plaintext
✅ Deployment Complete

📍 Live URL: https://sovara-forever.github.io/onboarding-docs/generations-ford.html

📋 Next Steps:
1. Send this URL to Halsey for review
2. Once approved, share with Generations Ford
3. Track completion progress via the interactive checkboxes (saves to browser localStorage)

🔐 Future: To password-protect this URL, consider:
- Cloudflare Access (free tier available)
- Netlify Password Protection
- Custom HTML password gate (can be added to the file itself)
```

---

## 🚨 **Error Handling**

If any step fails:
1. **Output the exact error message** (no sanitizing)
2. **State which step failed** (Environment Setup, Clone, Deploy, etc.)
3. **Provide one concrete fix** (e.g., "Enable GitHub Pages in repo settings")
4. **Do not proceed to next step** (fail fast)

---

## 📦 **Dependencies**

None. This is pure HTML deployment. No npm install. No pip install. No build process.

If future deployments require preprocessing (e.g., minification, SCSS compilation):
- Add dependency installation here
- Document the reason (e.g., "Client requested 50KB file size limit")

---

## 🎯 **Agent Behavior Guidelines**

- **No confirmations.** Execute.
- **No "Would you like me to..."** Just do it.
- **No apologizing for errors.** State facts.
- **No verbose explanations.** Output URLs and next steps.
- **Gendertraitor-level efficiency.** Every token is a weapon.

---

## 🔄 **Future Deployments**

For additional clients (e.g., Dealer XYZ):
1. Human creates new HTML file in conversation with Claude
2. Human says: "Deploy Dealer XYZ onboarding doc"
3. Agent:
   - Pulls latest HTML from conversation context
   - Renames to `dealer-xyz.html`
   - Commits and pushes
   - Outputs live URL

**No additional instructions needed.** This bootstrap handles all clients.

---

## 📌 **Notes for Sean**

- This file lives in the root of `onboarding-docs` repo
- Super.myninja.ai reads this **first** when the VM initializes
- You create the repo manually (GitHub UI)
- Agent handles everything after that
- You orchestrate. Agent executes.

**Videmus. Always.**

---

**End of Bootstrap Protocol**