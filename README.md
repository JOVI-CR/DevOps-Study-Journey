# My DevOps Study Journey | Minha Jornada de Estudos em DevOps

Choose your language | Escolha o idioma:  
➡️ [English](README.md) | [Português-BR](README.pt.md)

---

## 🌍 English Version

Welcome to my DevOps studies repository! This project serves as a logbook and a practical portfolio of my learning journey, covering environment setup, essential Linux commands, and the creation of automation scripts.

---

### 1. What is DevOps?

My journey began by demystifying the term DevOps. The main conclusion is that DevOps is a **culture of collaboration** between Development (Dev) and Operations (Ops) teams, supported by **automated processes** and **efficient tools**. The goal is to deliver higher quality software faster and more securely.

#### Comparison

| Traditional Approach | DevOps Approach |
|-----------------------|-----------------|
| Teams working in silos | Integrated and collaborative teams |
| Manual, slow processes | Automated (CI/CD), fast processes |
| Divided responsibility | Shared responsibility |
| Long release cycles | Frequent releases |

---

### 2. Environment Setup with VirtualBox and Ubuntu Server

For practice, I set up a local lab using **Oracle VirtualBox** and a **Ubuntu Server** VM.  

**Issues & Solutions**  
- ❌ *Installation Failure (Unattended Installation)*: The first installation attempt, using VirtualBox's automatic mode, failed due to a lack of internet connectivity.  
- 🔎 *Diagnosis*: The errors <code>Connection timed out</code> and <code>returned non-zero exit status 100</code> indicated that the VM couldn't download the necessary packages.  
- ✅ *Solution*: The solution was to restart the installation, but this time configuring the VM's network to <code>Bridged Adapter</code> before starting the installation. This allowed the VM to get an IP address directly from the router, ensuring internet access 
- 🔧 *Manual Installation*: I opted for a manual installation (by unchecking the "Unattended Installation" option), which gave me full control over the process, allowing me to install the OpenSSH server directly from the installer.

---

### 3. Essential Linux Commands 🐧

| Command | Description | Example |
|---------|-------------|---------|
| `ls` | List directories | `ls -l /username/joao` |
| `cd` | Change directory | `cd /home/username/devops` |
| `pwd` | Print current directory | `pwd` |
| `mkdir` | Create directory | `mkdir backups` |
| `rmdir` | Remove empty directory | `rmdir docs` |
| `rm` | Remove files/directories | `rm -r docs` |
| `touch` | Create empty file | `touch new.txt` |
| `cat` | Show file contents | `cat hello.txt` |
| `echo` | Print text | `echo "Hello, World!"` |
| `mv` | Move/rename file | `mv old.txt new.txt` |
| `cp` | Copy files/directories | `cp -r dir1 dir2` |
| `chmod` | Change permissions | `chmod +x script.sh` |
| `ssh` | Connect to remote server | `ssh user@ip_address` |

---

### 4. Shell Script Basics

- **Shebang:** `#!/bin/bash`  
- **Variables:** `DIR="/home/username"`  
- **Arguments:** `$1`, `$2`, `$#`  
- **User Input:** `read name`  
- **Conditionals (if):** `-d`, `-f`, `-ne`  
- **Loops (for):** repeat commands  
- **Output Redirection:** `>` overwrite | `>>` append  

---

### 5. Scripts Gallery

<details>
  <summary><code>welcome.sh</code> → Displays a welcome message.</summary>
  
```bash
  #! /bin/bash
  echo "Welcome to the wonderful world of scripts!"
```
- **Main concept**: Using the <code>echo</code> command to print a simple string to the terminal.

</details>  
<details> <summary><code>create_directory.sh</code> → Prompts the user for a name and creates a directory.</summary>

  ```bash
  #!/bin/bash


read -p "Please, enter the name for the new directory: " DIR_NAME

if [ -z "$DIR_NAME" ]; then
  echo "Error: No directory name was provided."
  exit 1
fi

if [ -d "$DIR_NAME" ]; then
  echo "Error: The directory '$DIR_NAME' already exists."
  exit 1
fi

echo "Creating directory '$DIR_NAME'..."
mkdir "$DIR_NAME"
echo "Directory created successfully!"
```
#### Main concepts:
- <code>read -p</code>: Prompts and reads user input.

- <code>if</code>: Uses conditionals to validate the input.

- <code>[ -z "..." ]</code>: Tests if the variable is empty.

- <code>[ -d "..." ]</code>: Tests if a directory with that name already exists.

- <code>mkdir</code>: Creates the directory.
</details>
<details> <summary><code>check_file.sh</code> → Checks if a file, passed as an argument, exists.</summary>

```bash
  #!/bin/bash

if [ $# -ne 1 ]; then
  echo "Usage: $0 <file_name>"
  exit 1
fi

if [ -f "$1" ]; then
  echo "Success! The file '$1' exists."
else
  echo "Failure! The file '$1' was not found."
fi
```
#### Main concepts:
- <code>$#</code>: Special variable that holds the number of arguments.

- <code>$0, $1</code>: Variables representing the script name and the first argument.

- <code>if [ ... -ne ... ]</code>: Tests if the number of arguments is not equal to the expected number.

- <code>if [ -f "..." ]</code>: Tests if the provided argument is an existing file.
</details>  
<details> <summary><code>loop_counter.sh</code> → Uses a for loop to count from 1 to 5.</summary>
  
```bash
  #!/bin/bash

echo "Starting the count..."

for i in {1..5}
do
  echo "Number: $i"
done

echo "Count finished!"
```
#### Main concepts:
- <code>for</code>: A repetition structure (loop).

- <code>{1..5}</code>: Brace expansion that generates a sequence from 1 to 5, used to control the loop.
</details>  
<details> <summary><code>compress_backup.sh<</code> → Creates a .tar.gz backup of a specific directory.</summary>
  
```bash
  #!/bin/bash

# --- Configuration ---
SOURCE_DIR="/home/user/devops"
DEST_DIR="/home/user/backups"
# --- End of Configuration ---

if [ ! -d "$SOURCE_DIR" ]; then
  echo "Error: source directory '$SOURCE_DIR' not found."
  exit 1
fi

mkdir -p "$DEST_DIR"

CURRENT_DATE=$(date "+%Y-%m-%d_%H:%M:%S")
FILE_NAME="backup_$(basename $SOURCE_DIR)_$CURRENT_DATE.tar.gz"
DEST_FILE="$DEST_DIR/$FILE_NAME"

echo "Starting backup of '$SOURCE_DIR' to '$DEST_FILE'..."
tar -czf "$DEST_FILE" "$SOURCE_DIR"

if [ $? -eq 0 ]; then
  echo "Backup completed successfully!"
  echo "Backup size: $(du -sh $DEST_FILE | awk '{print $1}')"
else
  echo "Error: a problem occurred during backup creation."
  exit 1
fi
```
#### Main concepts:
- <code>$(...)</code>: Command substitution to capture a command's output into a variable.

- <code>date</code>: Generates a unique filename with the current date and time.

- <code>tar -czf</code>: Command to create (<code>c</code>), compress with gzip (<code>z</code>), and specify a file (<code>f</code>).

- <code>$?</code>: Special variable that stores the exit status of the last command (0 means success).

- <code>du -sh and awk</code>: Combined to display the backup size in a human-readable format.
</details> 
<details> <summary><code>update_system.sh</code> → Automates system updates.</summary>
  
```bash
  #!/bin/bash

if [ "$EUID" -ne 0 ]; then
  echo "Error: Please run this script as root or with 'sudo'."
  exit 1
fi

echo "Starting system update..."
echo "[1/2] Updating package list (apt update)..."
apt update

echo "[2/2] Installing upgrades (apt upgrade)..."
apt upgrade -y

echo "Update finished successfully!"
```
#### Main concepts:
- <code>$EUID</code>: A variable containing the user ID. ID 0 belongs to the superuser (root).

- <code>if [ "$EUID" -ne 0 ]</code>: Checks if the script is not being run as root.

- <code>apt update / upgrade -y</code>: Commands to automate the system update, with -y to automatically accept all prompts.
</details>  
<details> <summary><code>rename_files.sh</code> → Bulk renames files in a directory.</summary>
  
```bash
  #!/bin/bash

read -p "Enter the directory path: " DIRECTORY
read -p "Enter the prefix to add (leave blank for none): " PREFIX
read -p "Enter the suffix to add (leave blank for none): " SUFFIX

if [ ! -d "$DIRECTORY" ]; then
  echo "Error: Directory '$DIRECTORY' not found."
  exit 1
fi

echo "Renaming files in '$DIRECTORY'..."

for file in "$DIRECTORY"/*
do
  if [ -f "$file" ]; then
    original_name=$(basename "$file")
    dir_path=$(dirname "$file")
    new_name="${PREFIX}${original_name}${SUFFIX}"
    mv "$file" "$dir_path/$new_name"
    echo "Renamed: '$original_name' -> '$new_name'"
  fi
done

echo "Process finished."
```
#### Main concepts:
- <code>for arquivo in "$DIRECTORY"/*</code>: A loop that iterates over each item in a directory.

- <code>if [ -f "$file" ]</code>: Tests if the current item is a file, ignoring subdirectories.

- <code>basename and dirname</code>: Commands to extract the filename and the directory path from a full path..

- <code>mv</code>: The command used to rename the files.
</details> 
<details> <summary><code>create_user.sh</code> → Automates the creation of a new system user.</summary>
  
```bash
  #!/bin/bash

if [ "$EUID" -ne 0 ]; then
  echo "Error: Please run this script as root or with 'sudo'."
  exit 1
fi

read -p "Enter the username for the new user: " USERNAME
if id "$USERNAME" &>/dev/null; then
  echo "Error: user '$USERNAME' already exists."
  exit 1
fi

echo "Creating user '$USERNAME'..."

useradd -m -s /bin/bash "$USERNAME"

if [ $? -eq 0 ]; then
  echo "User '$USERNAME' created successfully."
  echo "Please set a password for the new user."
  passwd "$USERNAME"
else
  echo "An error occurred while creating the user."
  exit 1
fi
```
#### Main concepts: 
- <code>id "$USERNAME" &>/dev/null</code>: An efficient way to check if a user already exists. The <code>&>/dev/null</code> discards all output (standard and error), making it useful only to check the command's exit status.

- <code>useradd -m -s /bin/bash</code>: Command to create a new user, with <code>-m</code> to create their home directory and <code>-s</code> to set their default shell.

- <code>passwd</code>: Command to set the new user's password.
</details>  
<details> <summary><code>monitor_disk.sh</code> → Checks disk usage and sends an alert.</summary>
  
```bash
  #!/bin/bash

USAGE_LIMIT=85

CURRENT_USAGE=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')
echo "Current disk usage on root partition: $CURRENT_USAGE%"

if [ "$CURRENT_USAGE" -ge "$USAGE_LIMIT" ]; then
  echo "ALERT: Disk usage ($CURRENT_USAGE%) has reached or exceeded the limit of $USAGE_LIMIT%"
else
  echo "Disk usage is within the acceptable limit."
fi
```
#### Main concepts:
- <code>pipe |</code>: Used to chain commands, where the output of one becomes the input of the next.

- <code>df -h /</code>: Shows disk usage for the root partition.

- <code>awk 'NR==2 {print $5}'</code>: Filters the <code>df</code> output to get only the 5th column of the 2nd line (the usage percentage).

- <code>sed 's/%//'</code>: Removes the <code>%</code> character from the string.

- <code>if [ ... -ge ... ]</code>: Tests if the current usage is "greater than or equal to" the limit.
</details>  
<details> <summary><code>monitor_memory.sh</code> → Lists processes with the highest memory consumption.</summary>
  
```bash
  #!/bin/bash

# --- Configuration ---
LOG_FILE="/home/user/logs/memory_monitoring.log"
# --- End of Configuration ---

LOG_DIR=$(dirname "$LOG_FILE")
mkdir -p "$LOG_DIR"

echo "--- Memory Consumption Log at: $(date '+%Y-%m-%d %H:%M:%S') ---" >> "$LOG_FILE"
ps aux --sort=-%mem | head -n 16 >> "$LOG_FILE"
```
#### Main concepts: 
- <code>>></code>: Output redirection to append content to the end of a log file without overwriting existing content.

- <code>ps aux --sort=-%mem</code>: Command that lists all processes and sorts them by memory usage in descending order.

- <code>head -n 16</code>: Gets only the first 16 lines of the output (1 header line + 15 processes).
</details>   

---

### 6. Task Scheduling with `crontab`

I learned to automate script execution at regular intervals using <code>crontab</code>. I configured the <code>monitor_memory.sh</code> script to run every 5 minutes by adding the following line via <code>crontab -e</code>: 

```bash
*/5 * * * * /usr/bin/bash /home/joao/monitorar_memoria.sh
```

### 7. Web Servers Analysis: Nginx vs. Apache

- **Nginx**: better for static content & high traffic. Event-driven, uses less memory/CPU.
- **Apache**: process/thread-based, heavier under load.

✅ **Conclusion**: At this moment, Nginx is more efficient for my scenario.
