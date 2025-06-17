# Http_Log_Analysis_With_Splunk

# 📊 Splunk Data Analysis Project

*A Step-by-Step Guide to Installing Splunk, Importing Data, and Running Basic SPL Queries on Windows 11*

---

## 📌 Overview

This project documents my hands-on experience using **Splunk Enterprise** on **Windows 11**, ideal for **beginners** looking to explore Splunk fundamentals. It covers:

* ✅ Installation & Setup
* ✅ Logging In & Navigating the UI
* ✅ Importing/Uploading Sample Data
* ✅ Running Basic SPL (Search Processing Language) Queries
* ✅ Creating a Simple Dashboard

---

## 🛠 Installation & Setup

### 1. Download & Install Splunk Enterprise

* Downloaded from the [Splunk Official Site](https://www.splunk.com)
* Ran `splunk-9.x.x-windows-x64-release.msi` installer with default settings
* Installed to: `C:\Program Files\Splunk`

### 2. Start Splunk Services

```powershell
cd "C:\Program Files\Splunk\bin"
splunk start
```

* Accepted license agreement
* Created admin credentials

### 3. Access Splunk Web Interface

* URL: [http://localhost:8000](http://localhost:8000)
* Logged in with the credentials created during setup

---

## 📂 Importing Data into Splunk

### Option 1: Upload Sample Log File

* Clicked **"Add Data"** → **"Upload"**
* Selected a sample `access.log` (e.g., Apache/Nginx logs)
* Set:

  * **Source Type:** `access_combined`
  * **Index:** `web_http` (custom)

### Option 2: Monitor a Directory (Auto-Ingest)

* Go to: `Settings → Data Inputs → Files & Directories`
* Pointed to: `C:\logs\http\`
* Assigned **Source Type:** `access_combined`

---

## 🔍 Basic SPL (Search Processing Language) Queries

### 1. Count HTTP Methods (GET, POST, etc.)

```spl
index=web_http sourcetype=access_combined
| stats count by http_method
```

### 2. Top 10 Source IPs with Most Requests

```spl
index=web_http
| top limit=10 src_ip
```

### 3. Filter by Status Code (404 Errors)

```spl
index=web_http status_code=404
| table src_ip, uri, user_agent
```

### 4. Time-Based Traffic Analysis

```spl
index=web_http
| timechart span=1h count by http_method
```

*Visualized using a line chart.*

---

## 📊 Sample Dashboard

Dashboard panels created include:

* **HTTP Method Distribution** *(Pie Chart)*
* **Top Requested URIs** *(Bar Chart)*
* **Error Rate Over Time** *(Line Chart)*

---

## 🚀 Key Takeaways

* ✔ Splunk is easy to install but requires **proper data parsing**.
* ✔ Field extractions are crucial — use `| table _raw` to debug.
* ✔ SPL is powerful — start with simple queries (`stats`, `top`, `timechart`).

---

## 📥 Resources

* [Splunk Official Documentation](https://docs.splunk.com)
* [SPL Quick Reference Guide (PDF)](https://docs.splunk.com/images/0/07/SPL_Quick_Reference.pdf)

---

> 💡 Feel free to fork this project and use it as a starting point for your own Splunk experiments!
