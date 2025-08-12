# osTicket: Prereqs & Installation (Full Walkthrough)

This repo documents, step‑by‑step, how to deploy **osTicket** (open‑source help desk) on a Windows VM, like an entry‑level IT project. It mirrors the structure you often see on GitHub: headings + screenshots with short captions.

> **What you’ll practice**
> - Spinning up a Windows VM (Azure)
> - Enabling IIS (web server) + required Windows Features
> - Installing PHP, MySQL, and osTicket
> - Basic configuration & verification
> - Taking/organizing screenshots and writing a clean README

---

## ⚙️ Environments & Technologies Used
- **Microsoft Azure** – Virtual Machine (Windows)
- **Windows 10/11 or Windows Server** – OS for hosting IIS
- **IIS (Internet Information Services)** – Web server role
- **PHP** – Scripting runtime for osTicket
- **MySQL (or MariaDB)** – Database server
- **HeidiSQL** – GUI to manage MySQL (optional but helpful)
- **osTicket** – Ticketing/help desk application

## 🖥️ Operating Systems Used
- Windows 10/11 (Pro) *or* Windows Server 2019/2022

## ✅ Prerequisites
- Azure account (free trial is fine)
- GitHub account
- Git (optional if you upload via GitHub web UI)
- A text editor (VS Code recommended)

---

## 📸 Screenshots Index
> Replace these image links with your own after you take screenshots on each step.
1. Azure VM created – `images/01-azure-vm-created.png`
2. Windows Features (IIS/Web Management) – `images/02-iis-features.png`
3. PHP installed & verified with phpinfo – `images/03-phpinfo.png`
4. MySQL installed – `images/04-mysql-installed.png`
5. HeidiSQL connected – `images/05-heidisql.png`
6. osTicket files in `C:\inetpub\wwwroot\` – `images/06-osticket-files.png`
7. osTicket installer page loads – `images/07-installer.png`
8. Installation complete / login – `images/08-installed.png`

---

## Step 1 — Create the VM (Azure)
**Why:** We need a computer in the cloud to host the help desk.
1. In Azure, create a **Windows** VM (size: `Standard_B1s` or better).  
2. Allow **RDP (3389)** inbound in the NSG so you can log in.  
3. Note its **public IP** and the **username/password** you set.  
_Screenshot:_ `images/01-azure-vm-created.png`

## Step 2 — Enable IIS + Required Windows Features
**Why:** osTicket is a web app. IIS serves web pages to browsers.
1. Open **Start → Turn Windows features on or off**.
2. Enable:
   - **Internet Information Services**
   - **Web Management Tools**
   - **World Wide Web Services → Application Development Features →** CGI, ISAPI Extensions, ISAPI Filters
3. Apply & restart if prompted.  
_Screenshot:_ `images/02-iis-features.png`

## Step 3 — Install PHP
**Why:** osTicket runs on PHP.
1. Download **PHP for Windows** (Non‑Thread Safe, x64).
2. Extract to `C:\PHP` and add to **System PATH**.
3. In IIS Manager → *Handler Mappings* → add **FastCGI** for `php-cgi.exe`.
4. Create a test file `C:\inetpub\wwwroot\phpinfo.php` with `<?php phpinfo(); ?>` and browse to `http://localhost/phpinfo.php`.  
_Screenshot:_ `images/03-phpinfo.png`

## Step 4 — Install MySQL (or MariaDB)
**Why:** osTicket stores data (tickets, users) in a database.
1. Install MySQL Server (note the **root** password).
2. Optional: Install **HeidiSQL** for easier DB management.  
_Screenshot:_ `images/04-mysql-installed.png` (MySQL) and `images/05-heidisql.png` (HeidiSQL)

## Step 5 — Deploy osTicket Files
**Why:** Put the app’s files where IIS can serve them.
1. Download osTicket and extract into `C:\inetpub\wwwroot\osticket`.
2. Ensure `IUSR`/`IIS_IUSRS` have read access (and write for setup).  
_Screenshot:_ `images/06-osticket-files.png`

## Step 6 — Run the Installer
**Why:** This wires PHP + IIS + MySQL together for osTicket.
1. Browse to `http://localhost/osticket/setup/`.
2. Provide DB details (host: `localhost`, user: `root` or a new user, db name: `osticket`).
3. Complete setup and then remove/secure the `setup` folder as prompted.  
_Screenshots:_ `images/07-installer.png`, `images/08-installed.png`

---

## 🧪 Verification
- You can log into **osTicket Admin Panel** and create a test ticket.
- The **phpinfo** page renders, proving PHP + IIS are wired up.
- MySQL is reachable, and the `osticket` database exists.

## 🧰 Repo Structure
```
.
├─ images/
│  ├─ 01-azure-vm-created.png
│  ├─ 02-iis-features.png
│  └─ …
├─ README.md
└─ .gitignore
```

## ✍️ How to Add Your Screenshots
1. Put your `.png` files into the `images/` folder.
2. In `README.md`, update each `images/XX-…png` path to match your file names.
3. Commit and push.

## ⬆️ Push This Project to GitHub
```
git init
git add .
git commit -m "Initial osTicket lab"
git branch -M main
git remote add origin <YOUR_REPO_URL>
git push -u origin main
```

---

## 🧠 Quick Glossary (Plain English)
- **VM (Virtual Machine):** A computer that lives inside another computer. Azure runs it for you.
- **IIS:** Windows’ built‑in web server; it sends web pages to people.
- **PHP:** A programming language osTicket is written in.
- **MySQL:** A database; think of it like super‑powered spreadsheets for apps.
- **HeidiSQL:** A friendly app to look at and edit the MySQL database.
- **Git/GitHub:** Version control + a website to store and show your project. You “commit” changes and “push” them online.
