
---

# Odoo Installation Process

**Created By:** Bijay Kumar Sahoo  
**Date:** 13/11/2024 (DD/MM/YYYY)

---

### Step 1: Install Required Software
1. **Visual Studio Code (VS Code)**
2. **NVM or Node.js**
3. **Python (latest version)**
4. **PostgreSQL**
5. **Git Bash**

---

### Step 2: Set Up PostgreSQL and Create a Database

#### Step 2.1: Locate the PostgreSQL `bin` Directory
Locate the PostgreSQL installation directory, typically found at:
```
C:\Program Files\PostgreSQL\<version>\bin
```

#### Step 2.2: Add PostgreSQL `bin` Directory to System PATH
1. Go to **Control Panel** > **System and Security** > **System**.
2. Click **Advanced system settings** on the left.
3. In the **System Properties** window, go to the **Advanced** tab and click on **Environment Variables**.
4. Under **System variables**, find the **Path** variable, select it, and click **Edit**.
5. Click **New** and paste the path to the PostgreSQL `bin` directory.
6. Click **OK** to close all windows.

#### Step 2.3: Verify the PATH Update
Open a command prompt and type:
```
psql --version
```

#### Step 2.4: Test PostgreSQL Connection
Attempt to connect to PostgreSQL:
```
psql -U postgres
```
Enter your password when prompted.

#### Step 2.5: Configure `pg_hba.conf`
Locate the `pg_hba.conf` file, usually in the PostgreSQL data directory:
```
C:\Program Files\PostgreSQL\<version>\data\pg_hba.conf
```
Ensure it has the following configuration:
```
# TYPE  DATABASE        USER            ADDRESS                 METHOD
local   all             all          127.0.0.1/32                md5
```

---

### Step 3: Download Odoo
before download odoo install requirements.txt of odoo 
```bash
pip install -r https://github.com/odoo/odoo/raw/18.0/requirements.txt
```

Clone the Odoo 18 repository using Git Bash or Command Prompt:
```bash
git clone https://github.com/odoo/odoo.git --branch 18.0 --depth 1
```

---

### Step 4: Configure Odoo

1. Copy `odoo.conf` from the `debian` folder to the main Odoo directory.
2. Open `odoo.conf` and add the following configuration:
   ```ini
   [options]
   admin_passwd = admin_password_here
   db_host = localhost
   db_port = 5432
   db_user = postgres
   db_password = your_postgres_password
   addons_path = addons
   logfile = C:\path\to\your\odoo.log  # Uncomment this line if you need logging.
   ```
   Replace `your_postgres_password` with the password you set for PostgreSQL.

---

### Step 5: Start Odoo

Run Odoo by opening Command Prompt in the Odoo directory and typing:
```bash
python odoo-bin -c odoo.conf
```

If this command doesn't work, try specifying the full path to the configuration file:
```bash
python odoo-bin -c C:\path\to\your\odoo\odoo.conf
```

---

### Step 6: Access Odoo
Open your web browser and navigate to:
```
http://localhost:8069
```

---

This guide should help you successfully install and set up Odoo 18 on your Windows system.

---

### Node Installation

#### Step 1: Download NVM
Visit the [NVM for Windows page](https://github.com/coreybutler/nvm-windows#readme) and scroll down to find the **NVM for Windows** section. Click **Download now**, which will redirect to the nvm-windows releases page. Scroll down and download **nvm-setup.exe**.

#### Step 2: Install NVM
1. Run **nvm-setup.exe** to install NVM.
2. Open Command Prompt and type:
   ```bash
   nvm -v
   ```
   to check the installed version of NVM.
3. Install Node.js version 18 by typing:
   ```bash
   nvm install 18
   ```
4. Set Node.js 18 as the active version:
   ```bash
   nvm use 18
   ```
5. Verify the Node.js installation:
   ```bash
   node -v
   ```

#### Step 3: Initialize Node Project
1. Create a new folder for your Node project.
2. Open Command Prompt, navigate to the new folder, and type:
   ```bash
   npm init -y
   ```
3. Check the folder to verify that a **package.json** file has been created.

Node.js 18 is now successfully installed.

---

This guide should help you successfully install and set up Odoo 18 and Node.js on your Windows system.
