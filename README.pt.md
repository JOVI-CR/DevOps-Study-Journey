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
| `ls` | Lista diretórios | `ls -l /home/username` |
| `cd` | Muda de diretório | `cd /home/username/devops` |
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
| `ssh` | Conecta a servidor remoto | `ssh user@ip_address` |

---

### ⚙️ 4. Fundamentos de Shell Script

- **Shebang:** `#!/bin/bash`  
- **Variáveis:** `DIRETORIO="/home/username"`  
- **Argumentos:** `$1`, `$2`, `$#`  
- **Entrada do Usuário:** `read nome`  
- **Condicionais (if):** `-d`, `-f`, `-ne`  
- **Loops (for):** repetição de comandos  
- **Redirecionamento de Saída:** `>` sobrescreve | `>>` adiciona  

---

### 5. Galeria de Scripts Desenvolvidos

<details>
  <summary><code>boas_vindas.sh</code> → Mensagem de boas-vindas</summary>
  
```bash
  #! /bin/bash
  echo "Boas-vindas ao meu script"
```
- **Conceito Principal**: Uso do comando <code>echo</code> para imprimir uma string (texto) simples no terminal.

</details>  
<details> <summary><code>criar_diretorio.sh</code> → Cria diretório com nome fornecido pelo usuário</summary>

  ```bash
  #!/bin/bash


read -p "Por favor, digite o nome do diretório a ser criado: " NOME_DIRETORIO

if [ -z "$NOME_DIRETORIO" ]; then
  echo "Erro: Nenhum nome de diretório foi fornecido."
  exit 1
fi

if [ -d "$NOME_DIRETORIO" ]; then
  echo "Erro: O diretório '$NOME_DIRETORIO' já existe."
  exit 1
fi

echo "Criando o diretório '$NOME_DIRETORIO'..."
mkdir "$NOME_DIRETORIO"
echo "Diretório criado com sucesso!"
```
#### Conceitos Principais:
- <code>read -p</code>: Solicita e lê uma entrada do usuário.

- <code>if</code>: Utiliza condicionais para validar a entrada.

- <code>[ -z "..." ]</code>: Testa se a variável está vazia.

- <code>[ -d "..." ]</code>: Testa se um diretório com aquele nome já existe.

- <code>mkdir</code>: Cria o diretório.
</details>
<details> <summary><code>verificar_arquivo.sh</code> → Verifica se arquivo existe</summary>

```bash
  #!/bin/bash

if [ $# -ne 1 ]; then
  echo "Uso: $0 <nome_do_arquivo>"
  exit 1
fi

if [ -f "$1" ]; then
  echo "Sucesso! O arquivo '$1' existe."
else
  echo "Falha! O arquivo '$1' não foi encontrado"
fi
```
#### Conceitos Principais:
- <code>$#</code>: Variável especial que conta o número de argumentos.

- <code>$0, $1</code>: Variáveis que representam o nome do script e o primeiro argumento.

- <code>if [ ... -ne ... ]</code>: Testa se o número de argumentos é diferente do esperado.

- <code>if [ -f "..." ]</code>: Testa se o argumento fornecido é um arquivo que existe.
</details>  
<details> <summary><code>loop_contador.sh</code> → Conta de 1 a 5 com for</summary>
  
```bash
  #!/bin/bash

echo "Iniciando a contagem..."

for i in {1..5}
do
  echo "Número: $i"
done

echo "Contagem concluída!"
```
#### Conceitos Principais:
- <code>for</code>: Estrutura de repetição (loop).

- <code>{1..5}</code>: Expansão de chaves que gera uma sequência de 1 a 5, usada para controlar o loop.
</details>  
<details> <summary><code>backup_com_compressao.sh</code> → Cria backup .tar.gz</summary>
  
```bash
  #!/bin/bash

# --- Configuração ---
DIRETORIO_ORIGEM="/home/joao/devops"
DIRETORIO_DESTINO="/home/joao/backups"
# --- Fim da Configuração ---

if [ ! -d "$DIRETORIO_ORIGEM" ]; then
  echo "Erro: o diretorio de origem '$DIRETORIO_ORIGEM' não foi encontrado."
  exit 1
fi

mkdir -p "$DIRETORIO_DESTINO"

DATA_ATUAL=$(date "+%Y%m%d_%H%M%S")
NOME_ARQUIVO="backup_$(basename $DIRETORIO_ORIGEM)_$DATA_ATUAL.tar.gz"
ARQUIVO_DESTINO="$DIRETORIO_DESTINO/$NOME_ARQUIVO"

echo "A iniciar o backup de '$DIRETORIO_ORIGEM' para '$ARQUIVO_DESTINO'..."
tar -czf "$ARQUIVO_DESTINO" "$DIRETORIO_ORIGEM"

if [ $? -eq 0 ]; then
  echo "Backup concluído com sucesso!"
  echo "Tamanho do backup: $(du -sh $ARQUIVO_DESTINO | awk '{print $1}')"
else
  echo "Erro: ocorreu um problema durante a criação do backup."
  exit 1
fi
```
#### Conceitos Principais:
- <code>$(...)</code>: Substituição de comando para capturar a saída de um comando em uma variável.

- <code>date</code>: Gera um nome de arquivo único com data e hora.

- <code>tar -czf</code>: Comando para criar (c), comprimir com gzip (z) e especificar um arquivo (f).

- <code>$?</code>: Variável especial que armazena o status de saída do último comando executado (0 significa sucesso).

- <code>du -sh e awk</code>: Combinados para exibir o tamanho do backup de forma legível.
</details> 
<details> <summary><code>atualizar_sistema.sh</code> → Automatiza atualização do sistema</summary>
  
```bash
  #!/bin/bash

if [ "$EUID" -ne 0 ]; then
  echo "Erro: Por favor, execute este script como root ou com 'sudo'."
  exit 1
fi

echo "A iniciar a atualização do sistema..."
echo "[1/2] A atualizar a lista de pacotes (apt update)..."
apt update

echo "[2/2] A instalar as atualizações (apt upgrade)..."
apt upgrade -y

echo "Atualização concluída com sucesso!"
```
#### Conceitos Principais:
- <code>$EUID</code>: Variável que contém o ID do usuário. O ID 0 pertence ao superusuário (root).

- <code>if [ "$EUID" -ne 0 ]</code>: Verifica se o script não está sendo executado como root.

- <code>apt update / upgrade -y</code>: Comandos para automatizar a atualização do sistema, com -y para aceitar automaticamente as confirmações.
</details>  
<details> <summary><code>renomear_arquivos.sh</code> → Renomeia arquivos em massa</summary>
  
```bash
  #!/bin/bash

read -p "Digite o caminho do diretório: " DIRETORIO
read -p "Digite o prefixo a ser adicionado (deixe em branco se não quiser): " PREFIXO
read -p "Digite o sufixo a ser adicionado (deixe em branco se não quiser): " SUFIXO

if [ ! -d "$DIRETORIO" ]; then
  echo "Erro: O diretório '$DIRETORIO' não foi encontrado."
  exit 1
fi

echo "A renomear os arquivos em '$DIRETORIO'..."

for arquivo in "$DIRETORIO"/*
do
  if [ -f "$arquivo" ]; then
    nome_original=$(basename "$arquivo")
    caminho_dir=$(dirname "$arquivo")
    novo_nome="${PREFIXO}${nome_original}${SUFIXO}"
    mv "$arquivo" "$caminho_dir/$novo_nome"
    echo "Renomeado: '$nome_original' -> '$novo_nome'"
  fi
done

echo "Processo concluído."
```
#### Conceitos Principais
- <code>for arquivo in "$DIRETORIO"/*</code>: Loop que itera sobre cada item dentro de um diretório.

- <code>if [ -f "$arquivo" ]</code>: Testa se o item atual é um arquivo, ignorando subdiretórios.

- <code>basename e dirname</code>: Comandos para extrair o nome do arquivo e o caminho do diretório de um caminho completo.

- <code>mv</code>: Comando usado para renomear os arquivos.
</details> 
<details> <summary><code>criar_usuario.sh</code> → Automatiza a criação de usuário</summary>
  
```bash
  #!/bin/bash

if [ "$EUID" -ne 0 ]; then
  echo "Erro: Por favor, execute este script como root ou com 'sudo'."
  exit 1
fi

read -p "Digite o nome de utilizador para o novo usuário: " NOME_USUARIO
if id "$NOME_USUARIO" &>/dev/null; then
  echo "Erro: o utilizador '$NOME_USUARIO' já existe."
  exit 1
fi

echo "A criar o utilizador '$NOME_USUARIO'..."

useradd -m -s /bin/bash "$NOME_USUARIO"

if [ $? -eq 0 ]; then
  echo "Utilizador '$NOME_USUARIO' criado com sucesso."
  echo "Por favor, defina uma senha para o novo utilizador."
  passwd "$NOME_USUARIO"
else
  echo "Ocorreu um erro ao criar o utilizador."
  exit 1
fi
```
#### Conceitos Principais: 
- <code>id "$NOME_USUARIO" &>/dev/null</code>: Forma eficiente de verificar se um usuário já existe. O &>/dev/null descarta toda a saída (normal e de erro) do comando, sendo útil apenas para verificar o status de saída.

- <code>useradd -m -s /bin/bash</code>: Comando para criar um novo usuário, com a opção -m para criar seu diretório home e -s para definir seu shell padrão.

- <code>passwd</code>: Comando para definir a senha do novo usuário.
</details>  
<details> <summary><code>monitorar_disco.sh</code> → Verifica uso do disco e alerta</summary>
  
```bash
  #!/bin/bash

LIMITE_USO=85

USO_ATUAL=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')
echo "Uso atual do disco na partição raíz: $USO_ATUAL%"

if [ "$USO_ATUAL" -ge "$LIMITE_USO" ]; then
  echo "ALERTA: o uso do disco ($USO_ATUAL%) atingiu ou excedeu o limite de $LIMITE_USO%"
else
  echo "O uso do disco está dentro do limite aceitável"
fi
```
#### Conceitos Principais:
- <code>pipe |</code>: Utilizado para encadear comandos, onde a saída de um se torna a entrada do próximo.

- <code>df -h /</code>: Mostra o uso do disco para a partição raiz.

- <code>awk 'NR==2 {print $5}'</code>: Filtra a saída do df para pegar apenas a 5ª coluna da 2ª linha (o percentual de uso).

- <code>sed 's/%//'</code>: Remove o caractere % da string.

- <code>if [ ... -ge ... ]</code>: Testa se o uso atual é "maior ou igual" (greater or equal) ao limite.
</details>  
<details> <summary><code>monitorar_memoria.sh</code> → Lista processos que mais consomem memória</summary>
  
```bash
  #!/bin/bash

# --- Configuração ---
LOG_FILE="/home/joao/logs/monitoramento_memoria.log"
# --- Fim da Configuração ---

LOG_DIR=$(dirname "$LOG_FILE")
mkdir -p "$LOG_DIR"

echo "--- Log de consumo de memória em: $(date '+%Y-%m-%d %H:%M:%S') ---" >> "$LOG_FILE"
ps aux --sort=-%mem | head -n 16 >> "$LOG_FILE"
```
#### Conceitos Principais: 
- <code>>></code>: Redirecionamento de saída para adicionar conteúdo ao final de um arquivo de log sem apagar o conteúdo que já possui.

- <code>ps aux --sort=-%mem</code>: Comando que lista todos os processos e os ordena pelo uso de memória de forma decrescente.

- <code>head -n 16</code>: Pega apenas as 16 primeiras linhas da saída (1 cabeçalho + 15 processos).
</details>  

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
