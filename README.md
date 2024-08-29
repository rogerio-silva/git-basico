# Treinamento Git: Fundamentos e Prática

## Aula Teórica 

### 1. Introdução ao Git
- **O que é Git?**
  - Git é um sistema de controle de versão distribuído, criado por Linus Torvalds em 2005. Ele permite que múltiplos desenvolvedores trabalhem simultaneamente em um projeto, mantendo um histórico completo de todas as mudanças realizadas no código-fonte.
- **Por que utilizar Git?**
  - Controle preciso das versões do projeto.
  - Facilita a colaboração entre equipes, permitindo que múltiplos desenvolvedores trabalhem em paralelo.
  - Histórico completo de todas as mudanças, com a possibilidade de reverter para versões anteriores.
- **Vantagens do Controle de Versão**
  - Rastreabilidade: cada alteração no código é registrada e pode ser rastreada.
  - Colaboração: múltiplos desenvolvedores podem trabalhar em diferentes partes do projeto ao mesmo tempo.
  - Backup: o código é seguro e pode ser restaurado em caso de falhas.

#### Exemplo Prático: Instalação do Git e configuração inicial (definir usuário e email)
- Comando para instalação do Git:
  - Windows: Usar o instalador oficial do Git.
  - Linux: `sudo apt -y install git`
  - MacOS: `brew install git`
  

- Configuração inicial do Git:
  ```bash
  git config --global user.name "Seu Nome"
  git config --global user.email "seu.email@exemplo.com"
  ```
- Testando a configuração:
  ```bash
  git config --list
  ```
  O comando `git config --list` exibe as configurações do Git, incluindo o nome e email do usuário.
  
### 2. Conceitos Básicos
- **Os três estados**
  - O Git possui três estados principais: _Working Directory_, _Staging Area_, e _Repository_.
    - _Working Directory_: é o diretório onde você trabalha no projeto, fazendo alterações nos arquivos.
    - _Staging Area_: é a área de preparação onde as mudanças são organizadas antes de serem commitadas.
    - _Repository_: é o repositório Git propriamente dito, onde as mudanças são salvas como commits.
    ![areas.png](figs/areas.png)

  - O fluxo de trabalho básico Git é algo assim:
    - Você modifica arquivos no seu diretório de trabalho.
    - Você prepara os arquivos, adicionando imagens deles à sua área de preparo. 
    - Você faz commit, o que leva os arquivos como eles estão na área de preparo e armazena essa imagens de forma permanente para o diretório do Git.

- **Repositórios (local e remoto)**
  - Um repositório Git armazena o histórico completo do projeto, incluindo todos os commits, branches, e tags. Existem repositórios locais (no seu computador) e remotos (em servidores, como GitHub, GitLab).
  - Para inicializar um repositório local:
    ```bash
      git init
    ```
  - Para exibir o estado do repositório: 
    ```bash
      git status
    ```
    O comando `git status` exibe informações sobre o estado atual do repositório, mostrando arquivos modificados, adicionados, e não rastreados.
  

- **Commits**
  - Um commit no Git é uma captura do estado do projeto num dado momento. Cada commit é identificado por um hash único e contém metadados sobre quem fez a mudança, quando e por quê.
  - Criação de um commit:
    ```bash
    echo "Algo" > arquivo.txt
    git status
    git add .
    git status
    git commit -m "Mensagem do commit"
    git status
    ```
    O código acima cria um arquivo chamado `arquivo.txt`, adiciona-o à área de _Staging_ com `git add .`, e faz um commit com a mensagem "Mensagem do commit".
    Para verificar cada passo, o comando `git status` pode ser utilizado para verificar o estado do repositório em cada etapa.
  
  - Para visualizar o histórico de commits:

    ```bash
    git log
    ```
    O comando `git log` exibe o histórico de commits, mostrando o hash do commit, autor, data, e mensagem associada a cada commit.
  

- **Branches**
  - Branches são ramificações do projeto que permitem trabalhar em diferentes versões simultaneamente. A branch principal é geralmente chamada de `main` ou `master`.
  - Para criar e alternar entre branches:
    ```bash
    # Para Criar uma nova branch
    git branch feature
    # Para Alternar entre branches
    git checkout feature
    # Para verificar as branches existentes
    git branch
    ```

#### Exemplo Prático: Inicializar um repositório, fazer o primeiro commit, criar e alternar entre branches
- Inicializar um repositório, adicionar um arquivo e fazer o commit:
  ```bash
  mkdir meu_projeto
  cd meu_projeto
  git init
  echo "Meu projeto Git" > arquivo.txt
  git add arquivo.txt
  git commit -m "Commit inicial"
  git branch nova-feature
  git checkout nova-feature
  echo "Criando novo arquivo" > arquivo_novo.txt
  git add arquivo_novo.txt
  git commit -m "Adicionando novo arquivo"
  ls
  git checkout master
  ls  
  ```
  No exemplo acima, um repositório Git é inicializado, um arquivo é adicionado e commitado, uma nova branch é criada e alternada, um novo arquivo é adicionado e commitado na nova branch, e a branch principal é alternada de volta.
  Os comandos `ls` são utilizados para listar os arquivos no diretório em cada etapa, observe que a branch `master` não possui o arquivo `arquivo_novo.txt` que foi adicionado na branch `nova-feature`.

### 3. Controle de Versões
- **Staging Area**
  - A Staging Area (ou Index) é a área de preparação onde as mudanças são organizadas antes de serem commitadas. Ela permite escolher quais mudanças serão incluídas no próximo commit.
  - Adicionar arquivos à Staging Area:
    ```bash
    git add arquivo.txt
    ```

- **Commit**
  - Um commit salva as mudanças que estão na Staging Area no histórico do repositório. Cada commit cria um ponto de restauração que pode ser utilizado posteriormente.
  - Criação de um commit:
    ```bash
    git commit -m "Mensagem descrevendo as mudanças"
    ```

- **Visualização de Histórico**
  - O comando `git log` exibe o histórico dos commits, mostrando o autor, data, e a mensagem associada a cada commit.
  - Exemplo de comando para visualizar o histórico de commits:
    ```bash
    git log
    ```


#### Exemplo Prático: Adicionar arquivos à Staging Area, fazer commits, e visualizar o histórico de commits com `git log`
- Adicionar um novo arquivo à Staging Area, fazer um commit, e visualizar o histórico:
  ```bash
  echo "Adicionando uma nova funcionalidade" > nova_feature.txt
  git add nova_feature.txt
  git commit -m "Adicionando nova funcionalidade"
  git log --oneline
    ```
  
O comando git log --oneline exibe um histórico simplificado, mostrando o hash abreviado e a mensagem do commit em uma única linha.

#### Exemplo prático: Desfazendo coisas

- **Desfazendo alterações não commitadas**
  - Para desfazer alterações não commitadas num arquivo:
    ```bash
    echo "Alteração não commitada" > arquivo.txt
    git status
    git checkout -- arquivo.txt
    git status
    ```
  - O comando `git checkout -- arquivo.txt` desfaz as alterações não commitadas no arquivo `arquivo.txt`, restaurando-o para o estado do último commit. Outra alternativa ao comando `git checkout -- arquivo.txt` é o `git restore arquivo.txt`.

- **Desfazendo alterações commitadas**
  - Para desfazer o último commit, mantendo as alterações no Working Directory:
    ```bash
    git reset HEAD~1
    ```
  - Para desfazer o último commit e descartar as alterações:
    ```bash
    git reset --hard HEAD~1
    ```
  - O comando `git reset HEAD~1` desfaz o último commit, mantendo as alterações no Working Directory. Já o comando `git reset --hard HEAD~1` desfaz o último commit e descarta as alterações, restaurando o repositório para o estado anterior ao commit.
  - **Atenção**: O comando `git reset --hard` é uma operação destrutiva e não pode ser desfeita. Utilize-o com cuidado.
  - Mas e se eu quiser desfazer o 'git reset --hard'? 
    - Se você fez um `git reset --hard` e se arrependeu, você pode tentar recuperar o commit perdido com o comando `git reflog`. O `git reflog` exibe o histórico de referências do Git, incluindo os commits que foram desfeitos.
    - Para recuperar um commit perdido, encontre o hash do commit no `git reflog` e utilize o comando `git reset --hard hash_do_commit`.

### 4. Trabalho Colaborativo
- **Repositórios Remotos**
  - Repositórios remotos permitem que o código seja compartilhado entre desenvolvedores via serviços como GitHub, GitLab, ou Bitbucket. Eles são utilizados para colaborar em equipe, mantendo uma cópia centralizada do projeto.
  - Para adicionar um repositório remoto ao seu repositório local:
    ```bash
    git remote add origin https://github.com/seu-usuario/seu-repositorio.git
    ```
  - Para verificar os repositórios remotos configurados:
    ```bash
    git remote -v
    ```

- **Push e Pull**
  - O comando `git push` envia as alterações do repositório local para o repositório remoto. Esse comando é utilizado para compartilhar suas mudanças com outros colaboradores.
    ```bash
    git push origin main
    ```
  - O comando `git pull` traz as alterações do repositório remoto para o repositório local, sincronizando o seu trabalho com as mudanças feitas por outros colaboradores.
    ```bash
    git pull origin main
    ```

- **Merges e Resolução de Conflitos**
  - O comando `git merge` é utilizado para combinar as mudanças de uma branch em outra. Isso é comum quando um trabalho feito em uma branch deve ser integrado de volta à branch principal.
    ```bash
    git merge feature-branch
    ```
  - Conflitos podem ocorrer durante um merge se as mesmas linhas de código foram modificadas de maneiras diferentes em duas branches. O Git marcará esses conflitos, e será necessário resolvê-los manualmente editando os arquivos e escolhendo quais mudanças devem ser mantidas.
  - Após resolver os conflitos, é necessário adicionar os arquivos corrigidos à Staging Area e criar um novo commit para finalizar o merge:
    ```bash
    git add arquivo_com_conflito.txt
    git commit -m "Resolvido o conflito entre a branch main e a feature-branch"
    ```

#### Exemplo Prático: Clonar um repositório remoto, fazer alterações, realizar push, e resolver conflitos durante um merge
- Clonar um repositório remoto e fazer alterações:
  ```bash
  git clone https://github.com/seu-usuario/seu-repositorio.git
  cd seu-repositorio
  echo "Alteração feita no clone" > alteracao.txt
  git add alteracao.txt
  git commit -m "Alteração feita no clone"
  git push origin main
    ```
  
Resolver um conflito durante um merge:
Suponha que um conflito ocorreu durante o merge. O Git identificará o conflito e marcará o arquivo conflitante.
Edite o arquivo para resolver o conflito, escolhendo as mudanças que devem ser mantidas.
Após resolver o conflito, adicione o arquivo à Staging Area e finalize o merge com um novo commit:
```bash
git add arquivo_com_conflito.txt
git commit -m "Resolvido o conflito"
```