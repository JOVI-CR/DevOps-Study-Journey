# 📘 Minha Jornada de Estudos em DevOps

Escolha o idioma | Choose your language:  
➡️ [Português-BR](README.pt.md) | [English](README.md)

---

Este repositório serve como um registro e guia dos meus estudos iniciais no mundo de **DevOps**, cobrindo a configuração do ambiente, comandos essenciais do Linux e a criação de scripts de automação.

---

### 1. O Que é DevOps?

Minha jornada começou por desmistificar o termo **DevOps**.  
A principal conclusão: **DevOps é uma cultura de colaboração entre as equipes de Desenvolvimento (Dev) e Operações (Ops)**, apoiada por processos automatizados e ferramentas eficientes.  

O objetivo é entregar software **de forma mais rápida, segura e com maior qualidade**.

#### Comparação

| Abordagem Tradicional | Abordagem DevOps |
|------------------------|------------------|
| Times separados em silos | Times integrados e colaborativos |
| Processo manual e lento | Processo automatizado (CI/CD), rápido |
| Responsabilidade dividida | Responsabilidade compartilhada |
| Lançamentos demorados | Lançamentos frequentes |

---

### 2. Configuração do Ambiente com VirtualBox e Ubuntu Server

Para praticar, configurei um laboratório local utilizando o **Oracle VirtualBox** e uma máquina virtual com **Ubuntu Server**.  

**Problemas & Soluções**  
- ❌ *Unattended Installation falhou* devido à falta de conectividade com a internet.  
- 🔎 Diagnóstico: `Connection timed out` → a VM não conseguia baixar os pacotes necessários.  
- ✅ Solução: configurar a rede como **Bridged Adapter**, garantindo IP válido e acesso à internet.  
- 🔧 Instalação Manual: optei pela instalação manual e adicionei o **OpenSSH** já durante o processo.

---

### 3. Comandos Essenciais do Linux 🐧

| Comando | Descrição | Exemplo |
|---------|-----------|---------|
| `ls` | Lista diretórios | `ls -l /home/joao` |
| `cd` | Muda de diretório | `cd /home/joao/devops` |
| `pwd` | Mostra diretório atual | `pwd` |
| `mkdir` | Cria diretório | `mkdir backups` |
| `rmdir` | Remove diretório vazio | `rmdir docs` |
| `rm` | Remove arquivos/diretórios | `rm -r docs` |
| `touch` | Cria arquivo vazio | `touch novo.txt` |
| `cat` | Exibe conteúdo de arquivo | `cat saudacao.txt` |
| `echo` | Imprime texto | `echo "Olá, Mundo!"` |
| `mv` | Move/renomeia arquivo | `mv antigo.txt novo.txt` |
| `cp` | Copia arquivos/diretórios | `cp -r dir1 dir2` |
| `chmod` | Altera permissões | `chmod +x script.sh` |
| `ssh` | Conecta a servidor remoto | `ssh joao@192.168.0.36` |

---

### ⚙️ 4. Fundamentos de Shell Script

- **Shebang:** `#!/bin/bash`  
- **Variáveis:** `DIRETORIO="/home/joao"`  
- **Argumentos:** `$1`, `$2`, `$#`  
- **Entrada do Usuário:** `read nome`  
- **Condicionais (if):** `-d`, `-f`, `-ne`  
- **Loops (for):** repetição de comandos  
- **Redirecionamento de Saída:** `>` sobrescreve | `>>` adiciona  

---

### 5. Galeria de Scripts Desenvolvidos

- `boas_vindas.sh` → Mensagem de boas-vindas  
- `criar_diretorio.sh` → Cria diretório com nome fornecido pelo usuário  
- `verificar_arquivo.sh` → Verifica se arquivo existe  
- `loop_contador.sh` → Conta de 1 a 5 com `for`  
- `backup_com_compressao.sh` → Cria backup `.tar.gz`  
- `atualizar_sistema.sh` → Automatiza atualização do sistema  
- `renomear_arquivos.sh` → Renomeia arquivos em massa  
- `criar_usuario.sh` → Automatiza a criação de usuário  
- `monitorar_disco.sh` → Verifica uso do disco e alerta se passar limite  
- `monitorar_memoria.sh` → Lista os 15 processos que mais consomem memória  

---

### 6. Agendamento de Tarefas com `crontab`

Exemplo: executar `monitorar_memoria.sh` a cada 5 minutos:  

```bash
*/5 * * * * /usr/bin/bash /home/joao/monitorar_memoria.sh
```

### 7. Análise de Servidores Web: Nginx vs. Apache

- **Nginx**: melhor para conteúdo estático e tráfego alto. Orientado a eventos, consome menos memória/CPU.
- **Apache**: baseado em processos/threads, menos eficiente sob carga.

✅ **Conclusão**: No meu cenário, o Nginx se mostrou mais eficiente.
