# 🚀 Setup Profissional de Desenvolvimento com WSL2 + Ubuntu no Windows

> Guia passo a passo para configurar um ambiente de desenvolvimento moderno, limpo e performático com **WSL2**, **Ubuntu**, **Node.js**, **Docker**, **Zsh** e **VS Code**.

---

## 🧠 Visão Geral

Esse setup foi feito para desenvolvedores que desejam:

- Ter um ambiente Linux completo **dentro do Windows** (via WSL2)  
- Usar **Docker**, **Node.js**, **pnpm/yarn**, **TypeScript**, **Git** e **VS Code** com performance nativa  
- Manter o sistema organizado e facilmente **reinstalável via snapshot**

---

## 🪟 1. Instalar o WSL2

Abra o **PowerShell como Administrador** e execute:

```bash
wsl --install
```

Após o processo, liste as distribuições disponíveis:

```bash
wsl --list --online
```

Escolha e instale o **Ubuntu 24.04 LTS**:

```bash
wsl --install -d Ubuntu-24.04
```

Se der erro de conexão (por exemplo `0x801901ad`), execute antes:
```bash
wsl --update
wsl --install -d Ubuntu
```

---

## 🐧 2. Acessar e atualizar o Ubuntu

Após a instalação, abra o terminal e atualize o sistema:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## ⚙️ 3. Instalar e configurar o Zsh + Oh My Zsh

Instale o Zsh:

```bash
sudo apt install -y zsh
```

Instale o **Oh My Zsh**:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Defina o Zsh como shell padrão:

```bash
chsh -s $(which zsh)
```

Feche e reabra o terminal.

---

## 🎨 4. (Opcional) Personalizar o Zsh

Edite o arquivo de configuração:

```bash
nano ~/.zshrc
```

Use o tema `powerlevel10k` para um visual moderno:
```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k
```

Em `~/.zshrc`, altere:
```
ZSH_THEME="powerlevel10k/powerlevel10k"
```

Ative plugins úteis:
```
plugins=(git docker npm node yarn)
```

Recarregue:
```bash
source ~/.zshrc
```

---

## 🧩 5. Instalar o NVM (Node Version Manager)

Baixe e instale:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

Carregue o NVM sem reiniciar:
```bash
. "$HOME/.nvm/nvm.sh"
```

Instale o Node.js LTS:
```bash
nvm install 22
nvm alias default 22
```

Verifique:
```bash
node -v
npm -v
```

---

## 🧰 6. Instalar ferramentas globais

```bash
npm install -g yarn pnpm eslint typescript ts-node nodemon
```

Verifique:
```bash
yarn -v
pnpm -v
```

---

## 🐳 7. Integrar com Docker Desktop

1. Instale o **Docker Desktop** no Windows.  
2. Vá em **Settings → Resources → WSL Integration**  
3. Ative:
   > ✅ *“Enable integration with my default WSL distro”*  
   e marque **Ubuntu-24.04**

Teste dentro do Ubuntu:
```bash
docker ps
```

Se der “permission denied”:
```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## 💻 8. VS Code + WSL

1. Instale o **VS Code** no Windows.  
2. Instale a extensão **Remote - WSL**.  
3. No terminal Ubuntu, abra o projeto:
   ```bash
   code .
   ```

O VS Code abrirá conectado ao ambiente Linux — tudo (Node, Docker, etc.) roda dentro do WSL.

---

## 📁 9. Estrutura de projetos

Crie uma pasta para seus projetos:

```bash
cd ~
mkdir projects
cd projects
```

💡 Use essa pasta para tudo que for **desenvolvimento**, pois o sistema de arquivos do WSL é muito mais rápido que o `/mnt/c/...`.

---

## 🔐 10. Variáveis de ambiente (IA / APIs)

Se for usar ferramentas como **OpenAI** ou **Claude**, adicione ao final do seu `~/.zshrc`:

```bash
export OPENAI_API_KEY="sua-chave"
export ANTHROPIC_API_KEY="sua-chave"
```

Recarregue:
```bash
source ~/.zshrc
```

---

## 💾 11. Backup (Snapshot do ambiente)

Antes de exportar, **feche o Docker Desktop e VS Code** e rode:

```bash
wsl --shutdown
wsl --export Ubuntu-24.04 C:\Backups\ubuntu24-setup.tar
```

Para restaurar no futuro:

```bash
wsl --import Ubuntu-24.04-Restore "C:\WSL\UbuntuRestore" C:\Backups\ubuntu24-setup.tar --version 2
```

---

## ⚡ 12. Ferramentas extras úteis

```bash
sudo apt install -y jq httpie tmux gh
```

| Ferramenta | Função |
|-------------|--------|
| `jq` | Manipular JSON no terminal |
| `httpie` | Testar APIs com visualização amigável |
| `tmux` | Sessões persistentes de terminal |
| `gh` | CLI do GitHub |

---

## ✅ 13. Checklist final

| Item | Status |
|------|---------|
| WSL2 + Ubuntu 24.04 instalado | ✅ |
| Zsh e Oh My Zsh configurados | ✅ |
| Node + NVM funcionando | ✅ |
| Docker integrado ao WSL | ✅ |
| VS Code conectado ao Ubuntu | ✅ |
| Pasta `projects` criada | ✅ |
| Backup (export) testado | ✅ |

---

## 🧠 Conclusão

Você agora tem um **ambiente Linux completo dentro do Windows**, com:
- Performance nativa pra Node.js / Docker  
- Terminal produtivo e bonito  
- Configuração reprodutível e segura  

💡 Ideal para qualquer stack JavaScript / TypeScript moderna (Next.js, Vite, Express, etc.)

---

> ✨ Criado por [Uande] — inspirado em boas práticas para desenvolvimento profissional no WSL2.
