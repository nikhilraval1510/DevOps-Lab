# Log Archive Tool

**Project URL:** [Insert your GitHub Repository URL here]

A robust command-line tool built in Bash that archives and compresses log directories into timestamped `.tar.gz` files. It automatically logs each archiving operation for easy auditing and system maintenance.

## Features

*   **Automated Compression:** Packages entire log directories (like `/var/log`) into space-saving `tar.gz` archives.
*   **Timestamping:** Appends precise date and time to both the archive filename and the audit log.
*   **Audit Logging:** Maintains a continuous `archive.log` file tracking what was archived, when, and where it was stored.
*   **Safe Execution:** Includes strict error handling (`set -euo pipefail`) and directory validation to prevent infinite loops or recursive archiving.

---

## 🚀 Quick Start Guide (For Beginners)

If you are a completely new user, follow these exact steps to download, configure, and execute the tool on your Linux or macOS machine.

### Step 1: Download the Project
Open your terminal and clone the repository to your local machine using Git:
```bash
git clone [https://github.com/nikhilraval1510/DevOps-Lab.git](https://github.com/nikhilraval1510/DevOps-Lab.git)
```

### Step 2: Navigate to the Folder
Change your current directory to the folder containing the script:
```bash
cd "DevOps-Lab/Projects/Log Archive Tool"
```

### Step 3: Prepare the Script
Clean up any hidden Windows-style line endings to prevent execution errors:
```bash
sed -i 's/\r$//' log-archive.sh
```
Next, grant the system permission to run the file as a program:
```bash
chmod +x log-archive.sh
```

### Step 4: Execute the Tool
Run the script by typing `./log-archive.sh` followed by the directory you want to compress. 

To test it on your system's main log folder (`/var/log`), use `sudo` to grant the necessary administrator permissions:
```bash
sudo ./log-archive.sh /var/log
```

### Step 5: Verify the Results
Once the script finishes, it will automatically create an `archives/` folder. You can verify your new backup and read the audit log by running:
```bash
ls -ltr archives/
cat archives/archive.log
```

---

## Archive Structure

The tool automatically generates an `archives/` directory in your current working space containing your compressed logs and the audit tracker:

```text
archives/
  ├── logs_archive_20260705_175620.tar.gz
  ├── logs_archive_20260706_000000.tar.gz
  └── archive.log
```

The `archive.log` file appends one line per successful run:
```text
[2026-07-05 17:56:20] Archived '/var/log' -> '/home/nikhil/DevOps-Lab/Projects/Log Archive Tool/archives/logs_archive_20260705_175620.tar.gz'
```

---

## Automation with Cron (Advanced)

You can automate this script to run on a set schedule using `cron`. To archive system logs without permission errors, the job must be added to the `root` user's crontab.

**1. Open the root crontab:**
```bash
sudo crontab -e
```

**2. Add the cron job:**
Add the following line to the bottom of the file to schedule the archive to run every night at exactly midnight. *(Note: Modify the path below to match where you cloned the repository, and ensure the path is enclosed in quotes).*
```text
0 0 * * * "/path/to/your/DevOps-Lab/Projects/Log Archive Tool/log-archive.sh" /var/log
```

**3. Save and Exit:** 
The archives will now generate automatically in the background every night.
