# Git e GitHub - Studies


## O que é versionamento de Código

É um sistema de controle de versão, que controla as versões de um arquivo ao longo do tempo.

- Registra o histórico de atualização de um arquivo;
- Gerencia quais foram as alterações, a data, o autor, etc...
- Organização, controle e segurança.


## Tipos de Sistemas de Controle de Versão

Dentre os sistemas de Controle de Versão ( VCS ), temos:

- VCS Centralizado ( CVCS )
  - Ex.: CVS, Subversion
- VCS Distribuídos ( DVCS )
  - Ex.: Git, Mercurial

### VCS Centralizado ( CVCS ):

Onde o banco de versões são salvos em um único servidor central, onde se acontecer algo e por um acaso o servidor ficar offline não se pode mexer no arquivo, com isso foi criado VCS Distribuídos.

### VCS Distribuídos ( DVCS ):

Onde os arquivos são no servidor central também são duplicados para os computadores locais de todos os desenvolvedores do projeto.
Clona o repositório completo, o que inclui o histórico de versões.

- Cada clone é como um backup
- Possibilita um fluxo de trabalho flexível
- Possibilidade de trabalhar sem conexão á rede


## O que é Git

Sistema de Controle de Versão Distribuído

- Gratuito e Open Source ( Código Aberto )
- Ramificações ( branching ) e fusões ( merging ) eficientes
- Leve e rápido

### Documentação: [Git - Documentation](https://git-scm.com/doc)

### Breve Histórico do Git:

2002 → O projeto de núcleo ( kernel ) do Linux, que é Open Source, começa a utilizar o BitKeeper, um DVCS proprietário.

2005 → Após alguns conflitos com a comunidade, o BitKeeper rescinde a licença gratuita. O que leva a Linux Torvalds, o criador do Linux, e sua equipe a desenvolverem sua própria ferramenta, o Git.


## O que é GitHub

Plataforma de hospedagem de código para controle de versão com Git, e colaboração.

- Comunidade ativa
- Utilizado mundialmente
- Mascote “Octocat”

### Documentação: [Documentação de ajuda do GitHub.com](https://docs.github.com/pt)

### Breve Histórico do GitHub:

2008 → Desenvolvido por Chris Wanstrath, J. Hyett, Tom Preston-Werner e Scott Chacon.

2018 → Vitima de um dos maiores ataques de DDoS ( ataque distribuído de negação de serviço ); Comprado pela Microsoft Corporation por US $ 7,5 bilhões.


## Configuraçãos e Autenticação Git

### Configurações iniciais

```bash
git config --global user.name "username"    # seta um username
git config --global user.email "email"      # seta um email
git config --global init.defaultBranch main # chama a branch principal de main

git config --global --list                  # lista as configs feitas
```

### Autenticando via Token

```bash
github.com → settings → Developer settings → Personal access tokens → token ( classic )


git config --global credential.helper cache # para salvar só durante um tempo
git config --global credential.helper store # para para sempre na maquina

git clone URL
# ira pedir o usuario do github e a senha que no lugar coloca o token
```


## Comandos Git

### Criando e clonando repositórios

```bash
git init # inicializa um repositório local com git
git remote add origin URL # para vincular um repositorio local com o do github
git branch -M main # muda o nome da brandh master para main
--------------------------------------------------------------------------------------------
git clone URL # clona um repositorio existente do github e ja inicializa o git
git clone URL NOVO-NOME # clone já com um novo nome
git clone URL --branch NOME-BRANCH --single-branch # clona do repositorio somente esta branch
```

### Salvando alterações no Repositório Local

```bash
git add ARQUIVO # Adiciona o arquivo a área de commit
git status # Mostra os status
git commit -m"MENSAGEM" # Commita os arquivos adicionados
git log # Mostra o commit
```

### Desfazendo alterações no Repositório Local

```bash
rm -rf .git # Exclui o arquivo Git
git restore ARQUIVO # Restaura o arquivo ao ultimo estado
git commit --amend -m"NOVA-MENSAGEM" # Altera a mensagem do Commit
git reset --ESCOLHA HASH # Retorna para um determinado commit
	--soft  # volta para o commit desejado e ja adiciona os arquivos no git add
	--mixed # volta para o commit desejado mas não adiciona os arquivos no git add
	--hard  # # volta para o commit desejado mas exclui os arquivos que não estavam no commit
git reset NOME-ARQUIVO  # tira o arquivo do git add
git restore --staged NOME-ARQUIVO # tira o arquivo do git add
git revert "commit" # reverte o que tinha feito no commit escolhido
```

### Enviando e baixando alterações com o Repositório Remoto

```bash
git push -u origin main # envia os arquivos para o github
git pull # puxa as alterações do github para o repositório local
```

### Trabalhando com Branches - Criando, mesclando, deletando e tratando conflitos

De maneira simples, uma Branch ( em tradução, “Ramo” ), é uma ramificação do seu projeto.

- É um ponteiro móvel para um commit no histórico do repositório;
- Quando você cria uma nova Branch a partir de outra existente, a nova se inicia apontando para o mesmo commit da Branch que estava quando foi criada.

```bash
git checkout -b NOME-BRANCH # Cria uma nova branch e altera para ela
git checkout NOME-BRANCH # altera entre as branchs
git branch -v # mostra o ultimo commit de cada branch
git merge NOME-BRANCH # mescla esta branch com a branch em que esta atualmente
git branch # lista as branchs
git branch -d NOME-BRANCH # exclui a branch
```

### Trabalhando com Branches - Comandos Úteis no Dia a Dia

```bash
git fetch origin main # baixa os arquivos do github mais não mescla
git fetch # traz todas as branchs do repositorio
git diff BRANCH1 BRANCH2 # mostra as diferenças entre as branchs
git merge origin/main
----------------------------------------------------------------------------------------------
git clone URL --branch NOME-BRANCH --single-branch # clona do repositorio somente esta branch
----------------------------------------------------------------------------------------------
git stash ARQUIVO # arquiva algo
git stash list # lista arquivos arquivados
git stash pop # tras o ultimo arquivo arquivado e exclui da pilha
git stash apply # tras o ultimo arquivo arquivado e mantem na pilha
```

### .gitignore
- O .gitignore serve para ignonorar certas pastas e arquivos que voce não queira que o git rastreie.


## Padronização de Commit

| Tipo de Commit | Descrição                                                                                                   |
| -------------- | ----------------------------------------------------------------------------------------------------------- |
| feat           | Adiciona uma nova funcionalidade ao projeto.                                                                |
| fix            | Corrige um bug ou problema no projeto.                                                                      |
| docs           | Altera a documentação do projeto. Ex.: README, comentários no código.                                       |
| style          | Realiza mudanças na aparência, sem alterar a funcionalidade.                                                |
| refactor       | Realiza mudanças no código que não alteram a funcionalidade.                                                |
| test           | Adiciona ou modifica testes no projeto.                                                                     |
| chore          | Indica mudanças no projeto que não afetem o sistema ou arquivos de testes. São mudanças de desenvolvimento. |
| build          | Utilizada para indicar mudanças que afetam o processo de build do projeto ou dependências externas.         |
| perf           | Indica uma alteração que melhorou a performance do sistema.                                                 |
| ci             | Utilizada para mudanças nos arquivos de configuração de CI.                                                 |
| revert         | Indica a reverão de um commit anterior.                                                                     |


## Github CLI
<b>Passo 1: Instalando o GitHub CLI</b><br>
O GitHub CLI é uma ferramenta que permite interagir com o GitHub diretamente do terminal. Para instalar o GitHub CLI, você pode seguir as instruções na página oficial do GitHub CLI.<br><br>

<b>Passo 2: Fazendo Login na Sua Conta do GitHub</b>
```bash
gh auth login
```
Siga as instruções na tela para concluir o processo de login. Logo veja uma descrição de cada etapa.
1. O GitHub CLI perguntará “Qual conta você gostaria de fazer login?”. Você terá duas opções: GitHub.com ou GitHub Enterprise Server. Na maioria dos casos, você vai querer selecionar GitHub.com.
2. O GitHub CLI perguntará “Como você gostaria de se autenticar?”. Você terá duas opções: Login com um navegador da web ou Colar um token de autenticação.
3. Se você escolher “Login com um navegador da web”, o GitHub CLI fornecerá um código de um único uso e abrirá uma janela do navegador para você concluir o login. Você precisará copiar o código, colá-lo na janela do navegador e seguir as instruções na tela para fazer login.
4. Se você escolher “Colar um token de autenticação”, você precisará gerar um token de acesso pessoal no GitHub e colá-lo no terminal.
5. Depois de concluir essas etapas, você estará autenticado no GitHub CLI e pronto para começar a usar os comandos do GitHub.<br><br>

<b>Passo 3: Criando um Novo Repositório no GitHub</b><br>
Agora que você está logado na sua conta do GitHub, pode criar um novo repositório. Para fazer isso, use o seguinte comando:
```bash
gh repo create <nome_do_repositorio>
```
* Substitua <nome_do_repositorio> pelo nome que você deseja dar ao seu repositório.<br>
Durante a criação do repositório, o GitHub CLI perguntará se você deseja adicionar um arquivo README, .gitignore ou licença. Você pode selecionar as opções de acordo com suas necessidades.<br><br>

<b>Passo 4: Enviando Seus Arquivos para o Repositório Remoto</b><br>
Por fim, você pode enviar seus arquivos para o repositório remoto. Para fazer isso, use os seguintes comandos:
```bash
git add .
git commit -m "primeiro commit"
git push -u origin main
```
* Esses comandos adicionam todos os arquivos do seu repositório local para a área de preparação, fazem um commit com a mensagem “primeiro commit” e enviam os arquivos para a branch main do seu repositório remoto.
* Lembre-se de substituir main pelo nome da branch que você deseja enviar, se não for main.
* Espero que este artigo tenha sido útil para você.

## Git Flow
### Regras basicas:
1. Minúsculas e separadas por hífen: Mantenha-se nas minúsculas para nomes de ramos e use hífens para separar palavras. Por exemplo, ou. `feature/new-loginbugfix/header-styling`
2. Caracteres Alfanuméricos: Use apenas caracteres alfanuméricos (a-z, A-Z, 0–9) e hífens. Evite pontuação, espaços, sublinhados ou qualquer caractere não alfanumérico.
3. Sem hífens contínuos: Não use hífens contínuos. pode ser confuso e difícil de ler. `feature--new-login`
4. Sem hífens de final: Não termine o nome da sua filial com um hífen. Por exemplo, não é uma boa prática. `feature-new-login-`
5. Descritivo: O nome deve ser descritivo e conciso, idealmente refletindo o trabalho realizado no ramo.

### Nomeclatura:
| Tipo de Branchs | Descrição                                                                                                                |
| --------------- | ------------------------------------------------------------------------------------------------------------------------ |
| main            | Branch principal, geralmente só é mandado novas realeses para ela.                                                       |
| develop         | Branch de desenvolvimento.                                                                                               |
| feature         | Usado para desenvolver novas funcionalidades que serão integradas em um futuro release.                                  |
| hotfix          | Criado para corrigir problemas críticos que foram identificados em produção.                                             |
| bugfix          | Usado para corrigir bugs detectados no ambiente de desenvolvimento ou QA (Controle de Qualidade).                        |
| task            | Usado para pequenas melhorias ou ajustes que não são novas funcionalidades completas, nem correções de bugs críticos.    |
| chore           | Usado para tarefas de manutenção como refatoração de código, atualizações de dependências, ou melhorias de configuração. |
| release         | Criado para preparar uma nova versão do software que será lançada. Serve como uma zona de testes final.                  |
| epic            | Utilizado para desenvolvimento de grandes funcionalidades ou projetos que abrangem várias features ou tarefas menores.   |
| improvement     | Focado em melhorias de funcionalidades já existentes.                                                                    |
