# 🚀 Jenkins Setup on EC2 with Git and Docker

This guide helps you set up Jenkins on an EC2 instance with Git and Docker integration.

```
git clone https://github.com/atulkamble/ec2-jenkins.git
cd ec2-jenkins
chmod +x deploy.sh
./deploy.sh
```
---

## 📌 Prerequisites

* **AWS EC2 Instance:** Amazon Linux 2023 (t3.large recommended)
* **Security Group Ports Open:**

  * SSH: 22
  * HTTP: 80
  * HTTPS: 443
  * Jenkins: 8080
* **Storage:** 30 GB SSD
* **Key Pair:** `jenkins.pem` (ensure secure permissions)

---

## ⚙️ Step 1: Connect to EC2 Instance

```bash
cd Downloads
chmod 400 jenkins.pem
ssh -i "jenkins.pem" ec2-user@<YOUR_EC2_PUBLIC_IP>
```

---

## 📦 Step 2: Install Required Packages

### 1. Update and Install Git

```bash
sudo yum update -y
sudo yum install git -y
git --version
```

### 2. Configure Git (Optional)

```bash
git config --global user.name "Swayamsiddha Savekar"
git config --global user.email "swayamsavekar21@gmail.com"
git config --list
```

### 3. Install Docker

```bash
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
```

### 4. Install Java (Amazon Corretto 21)

```bash
sudo dnf install java-21-amazon-corretto -y
java --version
```

### 5. Install Maven

```bash
sudo yum install maven -y
mvn -v
```

### 6. Install Jenkins

```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade -y
sudo yum install jenkins -y
jenkins --version
```

### 7. Add Jenkins User to Docker Group

```bash
sudo usermod -aG docker jenkins
```

---

## ▶️ Step 3: Start Jenkins

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

---

## 🌐 Step 4: Access Jenkins Web UI

Open your browser and go to:

```
http://<YOUR_EC2_PUBLIC_IP>:8080
```

Unlock Jenkins using the initial admin password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Paste the password into the Jenkins setup screen and proceed.

---

## ✅ Jenkins is now ready to use!
