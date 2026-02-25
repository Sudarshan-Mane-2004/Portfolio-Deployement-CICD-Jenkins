# 🚀 Static Portfolio Deployment using Jenkins CI/CD (GitHub Webhook + Target Server)

This project demonstrates how to deploy a static portfolio website using **Jenkins CI/CD pipeline** triggered by a **GitHub Webhook**, and automatically deploy the build to a **target server**.

---

## 🧱 Architecture

```
Developer → GitHub → Webhook → Jenkins → Target Server → Users
```

**Key Benefits**

* ✅ Fully automated CI/CD pipeline
* ✅ Real-time deployment using GitHub Webhook
* ✅ Zero manual deployment
* ✅ Production‑ready setup
* ✅ Interview‑ready DevOps project

---

# 📋 Prerequisites

Before starting, ensure you have:

* GitHub repository
* Jenkins server (installed & running)
* Target server (EC2 / VM / Linux server)
* Static website files (HTML, CSS, JS)
* Basic knowledge of Git and Linux

---

# 🔔 Step 1 — Configure Jenkins Server

## 1.1 Install Required Plugins

In Jenkins → **Manage Plugins**, install:

* Git plugin
* GitHub Integration plugin
* Pipeline plugin

---

## 1.2 Install Required Tools on Jenkins

On Jenkins server ensure:

* Git installed
* SSH access to target server
* Proper credentials configured

---

# 🚀 Step 2 — Prepare Target Server

On your target server:

```bash
sudo apt update
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```

Your web root will typically be:

```
/var/www/html
```

Ensure Jenkins can SSH into this server.

---

# 🔐 Step 3 — Add Jenkins Credentials

In Jenkins:

**Manage Jenkins → Credentials → Add Credentials**

Add:

* SSH username and private key for target server

Note the **credentials ID** — used in pipeline.

---

# ⚙️ Step 4 — Create Jenkins Pipeline Job

1. Jenkins → **New Item**
2. Select **Pipeline**
3. Configure Git repository URL
4. Save

---

# 🧩 Step 5 — Jenkins Pipeline Script

Example pipeline:

```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/YOUR_USERNAME/YOUR_REPO.git'
            }
        }

        stage('Deploy to Target Server') {
            steps {
                sshagent(['your-ssh-credential-id']) {
                    sh '''
                    scp -o StrictHostKeyChecking=no -r * user@TARGET_SERVER_IP:/var/www/html/
                    '''
                }
            }
        }
    }
}
```

Replace:

* `your-ssh-credential-id`
* `user`
* `TARGET_SERVER_IP`

---

# 🔗 Step 6 — Configure GitHub Webhook

1. Go to **GitHub repo → Settings → Webhooks**
2. Click **Add webhook**
3. Payload URL:

```
http://<jenkins-url>/github-webhook/
```

4. Content type: `application/json`
5. Select **Just the push event**
6. Save

✅ Now every push triggers Jenkins automatically.

---

# 🧪 Step 7 — Test the Pipeline

Push code:

```bash
git add .
git commit -m "trigger deployment"
git push origin main
```

Verify in **Jenkins → Build History**.

---

# 🔐 Production Hardening (Recommended)

* Enable Jenkins build triggers securely
* Restrict SSH access using key-based auth
* Add Nginx reverse proxy
* Enable HTTPS using Let's Encrypt
* Add Jenkins build notifications

---

# 🎯 Result

You now have:

* Automated CI/CD pipeline (Jenkins + Webhook)
* Automatic deployment to target server
* Zero‑touch production updates
* Portfolio accessible via target server public IP

---

# 👨‍💻 Author

**Sudarshan Mane**

* AWS & DevOps Enthusiast
* Jenkins CI/CD Portfolio Project

---

# ⭐ If this helped

Give the repo a star and connect on LinkedIn!
