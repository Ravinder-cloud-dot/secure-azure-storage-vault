Building a Secure Cloud Storage Vault with an IP Firewall

## 🏢 What is this project?
In a modern company, critical data assets (like database backups, accounting spreadsheets, or legal contracts) cannot just sit out in the open on the internet. If cloud storage folders are left accessible to the general public, hackers can scan and find them.

To solve this problem, I built a secure *Cloud Backup Vault* protected by an enterprise-grade *IP-Based Firewall*. 

Instead of leaving the data open, I configured a network-level wall that blocks the entire public internet, opening a private side door exclusively for my approved management laptop.

---

## 🛠️ Core Infrastructure Components Built
* *The Storage Container:* Deployed an Azure Blob Storage account using Locally-Redundant Storage (LRS) to keep costs optimized.
* *The Cloud Firewall:* Modified default network access policies from "All Networks" to "Selected Networks," strictly whitelisting my local workstation's public IPv4 address.
* *The Data Repository:* Provisioned a private asset container directory named company-backup-vault with disabled anonymous access.
* *Portal Management Data Upload:* Successfully populated the repository by securely routing a local data file (DailyReport.txt) from my whitelisted laptop through the firewall.

---

## 📐 Security Architecture Details
* *Whitelisted Management IP:* 122.173.25.51 (Exclusive laptop gateway)
* *Cloud Storage Account Name:* compantvault2026
* *Secure Vault Folder Directory:* company-backup-vault

---

## 🚀 Step-by-Step Validation & Testing

### 1. Provisioning the Secure Vault
I created the core storage resource container in Azure, manually overriding the cloud's default global exposure settings during creation to restrict all outside public internet pathways.

### 2. Whitelisting the Administrator
I added my laptop's public network footprint directly to the structural firewall rules, allowing my personal workspace device to safely view, update, and manage cloud files.

### 3. Structural Security Verification (The Mobile Phone Test)
To verify that the firewall was actively blocking unauthorized data requests, I logged into the subscription using a mobile device disconnected from home Wi-Fi (running on separate cellular data). 

* *The Laptop Result:* Accessed and viewed folder directory contents perfectly because the laptop IP was approved. ✅
* *The Mobile Device Result:* The Azure Firewall immediately intercepted the connection, denied data traversal, and threw a structural error stating: This request is not authorized to perform this operation. ❌

This successfully simulated a live real-world validation scenario, proving the infrastructure perimeter is fully secure.
