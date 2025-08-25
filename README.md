# Guia de Fluxo de Trabalho Git para Programadores

Este guia apresenta o fluxo básico de trabalho com Git e GitHub que todos os desenvolvedores da empresa devem seguir. É especialmente direcionado para programadores juniores e inclui explicações detalhadas de cada etapa.

## 📋 Índice

1. [Conceitos Básicos](#conceitos-básicos)
2. [Configuração Inicial](#configuração-inicial)
3. [Fluxo de Trabalho Principal](#fluxo-de-trabalho-principal)
4. [Comandos Essenciais](#comandos-essenciais)
5. [Como Fazer um Pull Request](#como-fazer-um-pull-request)
6. [Como Testar uma Branch de Colega](#como-testar-uma-branch-de-colega)
7. [Problemas Comuns e Soluções](#problemas-comuns-e-soluções)
8. [Boas Práticas](#boas-práticas)

## 🎯 Conceitos Básicos

### O que é uma Branch?
Uma **branch** (ramificação) é uma versão independente do código onde você pode trabalhar sem afetar o código principal. É como ter uma cópia do projeto onde você pode fazer alterações livremente.

### O que é um Pull Request?
Um **Pull Request (PR)** é uma solicitação para incorporar suas alterações ao código principal. É como dizer: "Olha, fiz essas alterações, podem revisar e aceitar?".

### Estrutura de Branches
- **main** ou **master**: Branch principal com código estável
- **develop**: Branch de desenvolvimento (se usada pela equipe)
- **feature/nome-da-feature**: Sua branch pessoal para desenvolver funcionalidades

## ⚙️ Configuração Inicial

### 1. Clone do Repositório
```bash
# Clone o repositório da empresa
git clone https://github.com/empresa/nome-do-projeto.git

# Entre na pasta do projeto
cd nome-do-projeto
```

### 2. Configuração do Git (primeira vez apenas)
```bash
# Configure seu nome
git config --global user.name "Seu Nome Completo"

# Configure seu email (use o mesmo do GitHub)
git config --global user.email "seu.email@empresa.com"
```

## 🔄 Fluxo de Trabalho Principal

### Etapa 1: Sempre Comece Atualizando o Main
Antes de começar qualquer trabalho novo, sempre atualize sua versão local do código principal:

```bash
# Vá para a branch main
git checkout main

# Baixe as últimas alterações
git pull origin main
```

**O que está acontecendo aqui?**
- `checkout main`: Muda para a branch principal
- `pull origin main`: Baixa todas as alterações que outros desenvolvedores fizeram no main

### Etapa 2: Crie Sua Branch Pessoal
```bash
# Crie e mude para uma nova branch
git checkout -b feature/nome-descritivo-da-tarefa
```

**Exemplos de nomes de branch:**
- `feature/login-usuario`
- `feature/cadastro-produto`
- `feature/correcao-bug-carrinho`

**O que está acontecendo?**
- `-b`: Cria uma nova branch
- O nome deve ser descritivo do que você vai desenvolver

### Etapa 3: Desenvolva Sua Funcionalidade
Agora você pode trabalhar normalmente no código. Faça suas alterações, teste, e quando terminar uma parte do trabalho:

```bash
# Veja quais arquivos foram modificados
git status

# Adicione os arquivos que você quer salvar
git add nome-do-arquivo.js
# OU adicione todos os arquivos modificados
git add .

# Faça um commit com uma mensagem descritiva
git commit -m "Adiciona funcionalidade de login"
```

**O que está acontecendo?**
- `git status`: Mostra quais arquivos foram modificados
- `git add`: Prepara os arquivos para serem salvos
- `git commit`: Salva as alterações com uma descrição

### Etapa 4: Envie Sua Branch para o GitHub
```bash
# Envie sua branch para o GitHub
git push origin feature/nome-da-sua-branch
```

**O que está acontecendo?**
- `push`: Envia suas alterações para o servidor do GitHub
- `origin`: Nome padrão do repositório remoto
- `feature/nome-da-sua-branch`: Nome da sua branch

### Etapa 5: Crie um Pull Request
1. Vá para o GitHub no seu navegador
2. Entre no repositório do projeto
3. Clique no botão **"Compare & pull request"** (aparece automaticamente)
4. Preencha o título e descrição do PR
5. Clique em **"Create pull request"**

## 🛠️ Comandos Essenciais

### Comandos de Status e Informação
```bash
# Ver situação atual dos arquivos
git status

# Ver histórico de commits
git log --oneline

# Ver diferenças nos arquivos modificados
git diff

# Ver em qual branch você está
git branch
```

### Comandos de Branch
```bash
# Listar todas as branches
git branch -a

# Mudar de branch
git checkout nome-da-branch

# Criar e mudar para nova branch
git checkout -b nova-branch

# Deletar branch local (após merge)
git branch -d nome-da-branch
```

### Comandos de Sincronização
```bash
# Baixar alterações do repositório remoto
git fetch

# Baixar e aplicar alterações
git pull origin main

# Enviar alterações
git push origin nome-da-branch
```

## 📝 Como Fazer um Pull Request

### Template de Descrição do PR
Sempre inclua essas informações no seu Pull Request:

```markdown
## Descrição
Breve descrição do que foi desenvolvido

## Alterações Feitas
- [ ] Funcionalidade X implementada
- [ ] Bug Y corrigido
- [ ] Testes adicionados

## Como Testar
1. Faça login no sistema
2. Acesse a página X
3. Clique no botão Y
4. Verifique se Z acontece

## Screenshots (se aplicável)
Cole aqui capturas de tela das alterações visuais
```

### Checklist Antes de Criar o PR
- [ ] Código testado localmente
- [ ] Sem erros no console
- [ ] Commit messages claras
- [ ] Branch atualizada com o main
- [ ] Arquivos desnecessários não incluídos

## 🧪 Como Testar uma Branch de Colega

Quando um colega abre um Pull Request, é importante testar o código dele localmente antes de aprovar. Aqui está como fazer isso:

### Cenário 1: Testar um Pull Request Existente

**Situação:** Seu colega criou um PR e você quer testar o código dele na sua máquina.

```bash
# 1. Primeiro, atualize suas informações sobre branches remotas
git fetch origin

# 2. Veja todas as branches disponíveis (incluindo as remotas)
git branch -a

# 3. Crie uma cópia local da branch do seu colega
git checkout -b feature/branch-do-colega origin/feature/branch-do-colega
```

**O que está acontecendo?**
- `git fetch`: Baixa informações sobre todas as branches do repositório remoto
- `git branch -a`: Lista todas as branches (locais e remotas)
- `git checkout -b`: Cria uma nova branch local baseada na branch remota

### Cenário 2: Testar Rapidamente (Sem Criar Branch Local)

Se você só quer dar uma olhada rápida no código:

```bash
# Baixe as informações mais recentes
git fetch origin

# Mude diretamente para a branch remota (modo "detached HEAD")
git checkout origin/feature/branch-do-colega

# ⚠️ ATENÇÃO: Neste modo, não faça commits! É só para testar.
```

### Cenário 3: Atualizar uma Branch que Você Já Está Testando

Se o colega fez novas alterações na branch dele:

```bash
# Na branch que você está testando
git pull origin feature/branch-do-colega
```

### Como Testar o Código

Após fazer checkout da branch do colega:

```bash
# 1. Instale dependências (se necessário)
npm install
# ou
pip install -r requirements.txt

# 2. Execute os testes
npm test
# ou
python -m pytest

# 3. Execute a aplicação
npm start
# ou
python app.py

# 4. Teste manualmente as funcionalidades descritas no PR
```

### Voltando para Sua Branch de Trabalho

Após terminar os testes:

```bash
# Volte para sua branch principal
git checkout main

# Ou volte para sua branch de trabalho
git checkout feature/minha-branch

# Se não precisar mais da branch de teste, delete ela
git branch -d feature/branch-do-colega
```

### Dicas para Review de Código

**O que verificar ao testar:**
- [ ] O código funciona conforme descrito no PR
- [ ] Não há erros no console/terminal
- [ ] A funcionalidade não quebra outras partes do sistema
- [ ] O código segue os padrões da equipe
- [ ] Os testes passam

**Como dar feedback:**
1. Vá para o GitHub
2. Entre no Pull Request
3. Clique em "Files changed"
4. Clique no "+" ao lado da linha para comentar
5. Escreva feedback construtivo

**Exemplos de bom feedback:**
- ✅ "Funciona bem! Só uma sugestão: poderia adicionar validação aqui?"
- ✅ "Testei e está funcionando. Encontrei um pequeno bug quando..."
- ❌ "Está errado"
- ❌ "Não gostei"

### Comandos Úteis para Review

```bash
# Ver diferenças entre sua branch e a do colega
git diff main..feature/branch-do-colega

# Ver apenas os arquivos que foram modificados
git diff --name-only main..feature/branch-do-colega

# Ver o histórico de commits da branch
git log main..feature/branch-do-colega --oneline

# Ver informações sobre a branch remota
git show-branch origin/feature/branch-do-colega
```

### Problemas Comuns ao Testar Branches de Colegas

**Problema:** "Branch não encontrada"
```bash
# Solução: Atualize as informações remotas
git fetch origin
git branch -a  # Verifique se a branch aparece agora
```

**Problema:** "Conflitos ao fazer checkout"
```bash
# Solução: Salve suas alterações primeiro
git stash  # Guarda suas alterações temporariamente
git checkout origin/feature/branch-do-colega
# Depois de testar:
git checkout sua-branch
git stash pop  # Recupera suas alterações
```

**Problema:** "Dependências diferentes"
```bash
# Solução: Reinstale dependências na branch do colega
npm install  # ou pip install, etc.
# Teste
# Depois volte para sua branch e reinstale novamente
git checkout sua-branch
npm install
```

## 🚨 Problemas Comuns e Soluções

### Problema 1: Conflito de Merge
**Sintoma:** Mensagem de conflito ao fazer pull ou merge

**Solução:**
```bash
# Atualize sua branch com o main
git checkout main
git pull origin main
git checkout sua-branch
git merge main

# Se houver conflitos, edite os arquivos manualmente
# Procure por <<<<<<< ======= >>>>>>>
# Escolha qual código manter e remova as marcações

# Após resolver conflitos
git add .
git commit -m "Resolve conflitos de merge"
```

### Problema 2: Esqueci de Criar Branch
**Sintoma:** Você fez alterações direto no main

**Solução:**
```bash
# Crie uma nova branch mantendo suas alterações
git checkout -b feature/minha-correcao

# Faça o commit normalmente
git add .
git commit -m "Minhas alterações"

# Volte para o main e resete
git checkout main
git reset --hard origin/main
```

### Problema 3: Commit com Erro
**Sintoma:** Fez commit mas quer alterar a mensagem ou adicionar arquivos

**Solução:**
```bash
# Alterar última mensagem de commit
git commit --amend -m "Nova mensagem correta"

# Adicionar arquivo ao último commit
git add arquivo-esquecido.js
git commit --amend --no-edit
```

### Problema 4: Branch Desatualizada
**Sintoma:** Sua branch está muito atrás do main

**Solução:**
```bash
# Na sua branch de trabalho
git checkout main
git pull origin main
git checkout sua-branch
git rebase main

# Se der conflito, resolva e continue
git rebase --continue
```

### Problema 5: Arquivo Não Deveria Ser Commitado
**Sintoma:** Commitou arquivo por engano (.env, node_modules, etc.)

**Solução:**
```bash
# Remove do próximo commit mas mantém no disco
git rm --cached arquivo-indesejado.txt

# Adicione ao .gitignore para evitar no futuro
echo "arquivo-indesejado.txt" >> .gitignore
git add .gitignore
git commit -m "Adiciona arquivo ao gitignore"
```

## ✨ Boas Práticas

### Commits
- **Faça commits pequenos e frequentes**
- **Use mensagens descritivas:**
  - ✅ "Adiciona validação de email no formulário"
  - ❌ "fix"
  - ❌ "alterações"

### Branches
- **Use nomes descritivos:**
  - ✅ `feature/carrinho-compras`
  - ❌ `minha-branch`
  - ❌ `teste123`

### Pull Requests
- **Sempre teste antes de abrir o PR**
- **Escreva descrição clara do que foi feito**
- **Responda aos comentários de code review**
- **Mantenha PRs pequenos (máximo 400 linhas alteradas)**

### Geral
- **Sempre puxe o main antes de começar novo trabalho**
- **Nunca trabalhe direto no main**
- **Delete branches após o merge**
- **Comunique problemas para o time**

## 🆘 Quando Pedir Ajuda

Procure ajuda quando:
- Aparecer mensagens de erro que não entende
- Não conseguir resolver conflitos
- Perder commits ou alterações
- Não conseguir fazer push
- O código não funcionar após merge

**Lembre-se:** É melhor pedir ajuda cedo do que quebrar o repositório!

## 📚 Comandos de Emergência

### Desfazer Alterações Locais
```bash
# Descartar alterações não commitadas
git checkout -- nome-do-arquivo
git checkout .  # todos os arquivos

# Voltar ao último commit
git reset --hard HEAD
```

### Recuperar Branch Deletada
```bash
# Ver commits recentes
git reflog

# Recuperar branch
git checkout -b nome-da-branch SHA-do-commit
```

---

## 🎯 Resumo do Fluxo

1. `git checkout main` → `git pull origin main`
2. `git checkout -b feature/minha-funcionalidade`
3. Desenvolver e testar
4. `git add .` → `git commit -m "Descrição clara"`
5. `git push origin feature/minha-funcionalidade`
6. Criar Pull Request no GitHub
7. Aguardar review e merge
8. Deletar branch local: `git branch -d feature/minha-funcionalidade`

**Lembre-se:** Sempre mantenha sua branch atualizada com o main e faça commits pequenos e frequentes!

---

*Este guia deve ser consultado sempre que tiver dúvidas. Mantenha-o sempre aberto durante o desenvolvimento!*
