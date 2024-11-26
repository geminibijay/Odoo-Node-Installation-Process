
---

# Odoo Installation Guide: Tested for Versions 16, 17, and 18.

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

#### Step 2.6: Open PowerShell or Command Prompt.
Run the psql command to access the PostgreSQL prompt (you might need to add PostgreSQL to your PATH if it's not recognized).

```bash
psql -U postgres
```
Create a New User (Role):

Run the following command to create a new user and set a password:
sql

```bash
CREATE USER odoo WITH PASSWORD 'yourpassword';
```

Create a New Database:

Run the following command to create a new database owned by the user you just created:
sql

```bash
CREATE DATABASE odoo<your_version> OWNER odoo;
```
Grant Permissions (Optional):

Make sure the user has all necessary permissions:
sql

```bash
ALTER ROLE odoo WITH LOGIN;
```

---

### Step 3: Download Odoo
If you want use Virtual Environment 

1. Open PowerShell as Administrator:

Search for "PowerShell" in the Start menu, right-click it, and choose "Run as Administrator."
Set the Execution Policy:

Run the following command to allow the execution of scripts. This command sets the policy to allow running scripts that you create:

```bash
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```
When prompted, type Y (Yes) to confirm.


Explanation of Execution Policies:

Restricted: No scripts can be run (default setting on Windows).
RemoteSigned: Allows scripts created on your local machine to run but requires downloaded scripts to be signed by a trusted publisher.
Activate the Virtual Environment Again:

Go back to your project directory and try activating the virtual environment again:

```bash
venv\Scripts\Activate
```

Revert Execution Policy (Optional):

If you want to reset the execution policy after you’re done working, run:

```bash
Set-ExecutionPolicy -ExecutionPolicy Restricted -Scope CurrentUser
```


before download odoo install requirements.txt of odoo in CMD 
```bash
pip install -r https://github.com/odoo/odoo/raw/<your_version>/requirements.txt
```

Clone the Odoo <your_version>repository using Git Bash or Command Prompt:
```bash
git clone https://github.com/odoo/odoo.git --branch <your_version> --depth 1
```

---

### Step 4: Configure Odoo

1. Copy `odoo.conf` from the `debian` folder to the main Odoo directory.
2. Open `odoo.conf` and add the following configuration:
   ```bash
      [options]
      db_host = localhost
      db_port = 5432
      db_user = odoo
      db_password = 12345
      db_name = False
      db_maxconn = 64
      //addons_path = C:\Users\Bijay\Desktop\demo\test\odoo\addons
      //logfile = C:\Users\Bijay\Desktop\demo\test\odoo\odoo.log
      //log_level = debug
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

### Error: Internal Server Error

This guide should help you successfully install and set up Odoo 18 and Node.js on your Windows system.

The "Internal Server Error" you're seeing can be caused by a variety of issues with Odoo's configuration or environment. Here's a step-by-step guide to diagnose and resolve the problem:

1. Check Odoo Logs for More Information
The error message you're seeing in the browser is quite general. To get more detailed information, you should check the Odoo logs.

In your odoo.conf file, you should have a logfile entry where Odoo writes logs (e.g., logfile = C:\Users\Bijay\Desktop\demo\test\odoo\odoo.log).
Open this log file (odoo.log) and check for any specific errors or stack traces that can provide more insight into what's causing the issue.
2. Verify Database Configuration
Sometimes, the error occurs due to issues with the database connection. Make sure that:

Your PostgreSQL service is running.
The db_user and db_password settings in your odoo.conf are correct and match your PostgreSQL credentials.
The db_host and db_port are set to localhost and 5432 (or the correct host/port if using a remote database).
3. Check for Missing Dependencies
If there are missing Python dependencies, Odoo will fail to start. To ensure all dependencies are installed:

Make sure you’ve activated your virtual environment (venv\Scripts\activate).
Run the following command to install all necessary dependencies:

```bash
pip install -r requirements.txt
```

4. Check Addons Path
Ensure that the addons_path is set correctly in your odoo.conf. This should point to the directory containing Odoo modules (e.g., addons). If the path is wrong or empty, Odoo may not be able to load necessary modules and fail to start.

Example:
```bash
addons_path = C:\Users\Bijay\Desktop\demo\test\odoo\addons
```

5. Database Initialization
If this is a fresh Odoo installation, the database might not be initialized properly. You can try running the following command to initialize the database:

```bash
python odoo-bin -c odoo.conf -d odoo18 --init=all
```
This command tells Odoo to initialize all the modules and create the necessary tables in the database.

6. Clear Cache/Temporary Files
Sometimes, Odoo can fail to start due to old cached files. You can try clearing the cache:

Delete the __pycache__ folders in the odoo directory.
Delete the contents of the odoo/filestore directory (make sure to back it up first if needed).

7. Check Permissions
Make sure that Odoo has the necessary read/write permissions for the directories involved, especially for the logs and database files.

8. Restart the Odoo Server
Once you’ve addressed potential issues, restart the Odoo server:

```bash
python odoo-bin -c odoo.conf
```

9. Try Debugging Mode
You can try running Odoo in debug mode to see more detailed error information in the browser. To do this, add the --debug option when starting the server:

```bash
python odoo-bin -c odoo.conf --debug
```

10. Check Browser Console
Additionally, inspect your browser's console (press F12 to open Developer Tools) for any additional error messages related to JavaScript or network issues.


