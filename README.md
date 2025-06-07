# Azure Sentinel Live RDP Attacks Home Lab

## 🧠 Purpose
Simulate real-world RDP brute-force attacks using an exposed Azure VM honeypot, extract logs via PowerShell, enrich data with geolocation, and visualize attacks on a world map in Microsoft Sentinel.

---

## 🛠️ Tools & Technologies

- **PowerShell:** Extract failed RDP logins
- **ipgeolocation.io:** Convert IPs to location
- **Azure Sentinel:** Monitor & visualize attacks
- **Log Analytics Workspace:** Store & query logs
- **Windows 10 VM:** Honeypot for incoming RDP attacks

---

## 🔧 Key Steps

### 1. Create a Public Azure VM Honeypot  
- Windows VM with **RDP port open (3389)**  
- **Firewall disabled** to allow brute force attempts  
- Enable logging for security events  


---

### 2. Set Up Log Analytics Workspace & Connect VM  
- Create a **Log Analytics Workspace**  
- Connect the VM to it for **centralized logging**

> ![Connect VM](https://i.imgur.com/fKHWoe0.png)  

---

### 3. Enable Microsoft Defender for Cloud  
- Ensure **all security events** are collected  
- Configure VM **monitoring agent**

> ![Defender Config](https://i.imgur.com/Brjfczf.png)  

---

### 4. Configure Microsoft Sentinel  
- Link Sentinel to your Log Analytics Workspace  
- Use Sentinel to build custom **KQL queries and dashboards**

> ![Microsoft Sentinel](https://i.imgur.com/HaGg6BJ.png)

---

### 5. Run PowerShell Script to Extract Failed Logins & Enrich with Geolocation  
- Extract failed RDP login events (`Event ID 4625`)  
- Query **ipgeolocation.io API**  
- Create a log file with IP, country, city, lat/long  

> ![Run Script](https://i.imgur.com/3gLgDup.png)  

---

### 6. Import the Log as a Custom Table in Log Analytics  
- Upload the `.log` file as a **custom log**  
- **Extract key fields** like IP, Country, City, Coordinates  

> ![Field Extraction](https://i.imgur.com/ipuwNdO.png)  

---

### 7. Create a Sentinel Workbook with Map Visualization  
- Query logs by coordinates  
- Visualize on a **world map** to see attack origins  

> ![World Map](https://i.imgur.com/mPgDumR.png)

---

## ✅ Results

- After 24 hours, attacks came from various global IPs.
- Real-time attack visualization helps demonstrate how vulnerable RDP is when exposed.

---

## 🔐 Notes
- Azure free tier available for testing  
- API key required from [ipgeolocation.io](https://ipgeolocation.io)  
- Disable this VM after the lab to avoid unnecessary billing and exposure
