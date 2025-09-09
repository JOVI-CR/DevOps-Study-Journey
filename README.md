# 📘 My DevOps Study Journey | Minha Jornada de Estudos em DevOps

Choose your language | Escolha o idioma:  
➡️ [English](README.md) | [Português-BR](README.pt.br)

---

## 🌍 English Version

This repository is a record and guide of my initial studies in **DevOps**, covering environment setup, essential Linux commands, and automation scripting.

---

### 1. What is DevOps?

My journey started by demystifying the term **DevOps**.  
The main conclusion: **DevOps is a culture of collaboration between Development (Dev) and Operations (Ops) teams**, supported by automated processes and efficient tools.  

The goal is to deliver software **faster, safer, and with higher quality**.

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
- ❌ *Unattended Installation failed* due to no internet connectivity.  
- 🔎 Diagnosis: `Connection timed out` → VM couldn’t download required packages.  
- ✅ Fix: configured **Bridged Adapter** to give the VM a valid IP and internet.  
- 🔧 Manual Installation: installed manually and added **OpenSSH** during setup.

---

### 3. Essential Linux Commands 🐧

| Command | Description | Example |
|---------|-------------|---------|
| `ls` | List directories | `ls -l /home/joao` |
| `cd` | Change directory | `cd /home/joao/devops` |
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
| `ssh` | Connect to remote server | `ssh joao@192.168.0.36` |

---

### ⚙️ 4. Shell Script Basics

- **Shebang:** `#!/bin/bash`  
- **Variables:** `DIR="/home/joao"`  
- **Arguments:** `$1`, `$2`, `$#`  
- **User Input:** `read name`  
- **Conditionals (if):** `-d`, `-f`, `-ne`  
- **Loops (for):** repeat commands  
- **Output Redirection:** `>` overwrite | `>>` append  

---

### 5. Scripts Gallery

- `boas_vindas.sh` → Welcome message  
- `criar_diretorio.sh` → Creates user-defined directory  
- `verificar_arquivo.sh` → Checks if file exists  
- `loop_contador.sh` → Counts 1–5 with `for`  
- `backup_com_compressao.sh` → Creates `.tar.gz` backup  
- `atualizar_sistema.sh` → Automates system update  
- `renomear_arquivos.sh` → Mass rename files  
- `criar_usuario.sh` → Automates user creation  
- `monitorar_disco.sh` → Disk usage check with alert  
- `monitorar_memoria.sh` → Lists top 15 memory-consuming processes  

---

### 6. Task Scheduling with `crontab`

Example: run `monitorar_memoria.sh` every 5 minutes:  

```bash
*/5 * * * * /usr/bin/bash /home/joao/monitorar_memoria.sh
```

### 7. Web Servers Analysis: Nginx vs. Apache

- **Nginx**: better for static content & high traffic. Event-driven, uses less memory/CPU.
- **Apache**: process/thread-based, heavier under load.

✅ **Conclusion**: At this moment, Nginx is more efficient for my scenario.
