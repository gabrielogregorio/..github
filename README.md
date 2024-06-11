## Informações de clone e fork
* Clone: Não consegue enviar modificações para o autor original. Se for projeto seu, ok, pode enviar, mas de terceiros não!
* Fork: Pega um projeto que não é seu e faz uma cópia para você. Pode unir com o repositório principal


## Github cli

```shell
# https://cli.github.com/manual/gh_repo_create
# create a repository interactively
gh repo create

# create a new remote repository and clone it locally
gh repo create my-project --public --clone

# create a remote repository from the current directory
gh repo create my-project --private --source=. --remote=upstream
```

## gitflow flow

```shell
# No Windows o gitflow já vem instalado com o git, mas no Linux/MacOs, é preciso instalar o git e o gitflow
sudo apt-get install git-flow

# Então é preciso inicializar o gitflow no repositório, use o comando abaixo
git flow init

 # O comando abaixo permite verificar as branchs, agora deveremos ter a branch main e a develop.
 # A main é sagrada e devemos nos aventurar na branch develop.
git branch

# Para trocar de branch precisamos executar o comando abaixo (Mas não mexa na Main por enquanto)
git checkout main

# Para enviar a branch develop para o GitHub devemos rodar o seguinte comando
git push -u origin develop

# A partir da branch develop, podemos criar as features da aplicação, com o gitflow podemos
# usar o seguinte comando
git flow feature start feature_gitflow

# Agora faça todos os commits necessários para a criação da feature
# Para finalizar a feature use o seguinte comando
git flow feature finish feature_gitflow

# Para a correção de bugs usamos a branch bugfix
git flow bugfix start bugfix_bug_y

# Para finalizar a branch use o seguinte comando
git flow bugfix finish bugfix_bug_y

# Quando a develop tiver features o suficiente para uma nova versão, iremos gerar um release
# Criando uma release seguindo o versionamento semântico
git flow release start 0.1.0

# Faça os testes, e quando estiver tudo ok é só finalizar a branch e fazer o push no repositório MAIN
git flow release finish '0.1.0' -m "Versão com novos recursos"

# Use o comando abaixo para verificar a releases.
git tag

# Para correção de bugs direto em produção usamos o seguinte comando (Use o versionamento Semântico)
git flow hotfix start x.x.x

# Após feito a correção, é preciso rodar o comando abaixo para finalizar a branch
git flow hotfix finish  x.x.x -m "Correçao no bug x"
```


## Versionamento Semântico    

As versões devem ser numeradas com números de 0 a 9, sendo no seguinte formato, Major.Minor.Patch, exemplo, 1.0.0     
| Item | Descrição |
|------|-----------|
| Major | Cada versão nova informa funcionalidade e códigos incompatíveis com os anteriores |
| Minor | Informa novas funcionalidades, sem incompatibilidade com versões anteriores |
| Patch | Indica correção de bugs, porém, sem quebra de compatibilidade |
| Pré-release | Versão ainda instável |     

```shell
# git config
git config --global user.name "Gabriel Gregório"  
git config --global user.email "youremail@email.com"   
git config --global core.editor code    

# show configs
git config user.email

# Ver uma lista de todas as definições
git config --list

# clone, set personal token (classic)
git clone

# salve crendential? 
git config --global credential.helper store

```

## git basics

### Estágios de um arquivo    
| Estágio | Descrição |
|---------|-----------|
| Untracked files | Arquivo não adicionado |
| Stage | Arquivo adicionado e preparado para o commit |
| Not Staged | Não preparado para o commit |
| commit | Criar um snapshot, uma versão |


```shell
# Inicializar um repositório
git init

# Ver o status
git status

# Fazendo um commit
git commit -m "Primeiro commit"


#Fazendo um commit e adicionando
git commit -am "Edit Readme"

# Buscar nos commits por algum commit que tenha o texto example
git log -S "example"

```
    
### git log

```shell
# Ver o histórico de commits
git log

# Definir limite de 3 commits
git log -3

# Mostrar apenas o hash com as mensagem
git log --oneline

# Ver diferenças entre commits
git show de99d4eda910dc834f414d8e59a5573a6e1cd21e

# Filtrar por um autor
git log --author='Kalia'

# Filtrar por expressão regular
git log --grep="bug"

# Colorir o histórico de commits
git log --all --decorate --oneline --graph

# Mostra a  Mensagem de todos os commits
git shortlog

# Quantidade de commits de cada autor
git shortlog -sn
```

## git diff

```shell
# Ver mudanças antes de commitar
git diff

# Ver apenas os nomes dos arquivos que foram modificado
git diff --name-only

```

## git restore 
```shell
# Restaura um arquivo modificado/apagado que não foi comitado
git restore file
```

## Branchs
Pode modificar os arquivos sem modificar no master

```shell
# Criando um brach
git checkout -b branchNovaBaseadaNaAtual

# lista as branchs
git branch

# Acessar um brach
git checkout master

# Apagar um branch
git branch -D bteste
```


## Não testados => git revert
Código quebrou, quero salvar a versão atual e voltar na antiga, depois volto nessa versão e verifico o problema, como fazer?


```shell
# Usando o git Revert commit
git revert 16110104a33763e5d109932edb1afaa43f21b0a3

# Apagar tags no local
git tag -d 1.0.1

# Apagar no remoto
git push origin :1.0.0

# Tirar o arquivo do stage (add)
git reset HEAD

# Depois do commit quebrar, pega um hash antes do commit bugado
git reset --soft 55ca76b8464fd8013861a69c768eb5a350e79455

# voltar antes do stage (add)
git reset --mixed 3b9bfc5feb84249255df03c8406dfb12c38ffaea

# Destruir o Commit por completo, altera o histórico e, portanto, para evitar conflitos não é interessante usá-lo
git reset --hard 3b9bfc5feb84249255df03c8406dfb12c38ffaea
```

## Resolução de conflitos no PR
```shell
[pr criado, myFeature com conflitos com develop]
git checkout myFeature
git fetch
git pull origin develop
[resolve]
git commit -m "my commit"
git push origin myFeature
```


## Outros comandos git

```shell
# Guarda informações que foram modificados, mas não adicionadas em um arquivo que eu posso chamar depois
git stash

# Aplica as modificações guardadas novamente
git stash apply

# Lista de todas as stash
git stash list

# Limpa todo o histórico
git stash clear

# Atalhos no git
git config --global alias.s status

# Renomeando uma branch, subindo a nova a removendo a antiga
git branch --move master main
git push -u origin main
git push origin --delete master

# Trabalhando com as tags.
git tag -a 1.0.0 -m "REAME FINALIZADO"
git push origin main --tags
```


## Links úteis    
* [gitignore](https://git-scm.com/docs/gitignore)
* [gitignore Templates](https://github.com/github/gitignore)



## Como unir o branch com o master
O merge cria um commit novo, junta o master com o brach secundário.

### Pros   
* Merge é uma operação não destrutiva, ele não estraga o histórico

### Contra   
* Precisa de um novo commit somente para juntar ambos.
* Deixa o histórico feio.
git merge bmerge

### Rebase   
O Rebase move o commit para a frente, modificando o histórico das brancs. Coloca na frente da fila

### pros    
* Evita commit extras
* Histórico linear

### Contras   
* Perde a ordem cronológica
* muda o histórico
    git rebase brebase

Rebase não polui o histórico, o merge da um histórico mais detalhado

---- 


## Adicionar o nome da branch no cli do Ubuntu 22

Abra o 
```bash
nano ~/.bashrc 
```

cole no final

```bash
# Show git branch name
force_color_prompt=yes
color_prompt=yes
parse_git_branch() {
 git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
if [ "$color_prompt" = yes ]; then
 PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '
else
 PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w$(parse_git_branch)\$ '
fi
unset color_prompt force_color_prompt
```

Recarregue o bash

```bash
source ~/.bashrc
```




-------------

# Configurando uma gpg key


Ver chaves disponíveis
```bash
gpg --list-secret-key --keyid-form LONG
```

Gerar uma chave RSA
```bash
gpg --full-generate-key
gpg (GnuPG)...
This is free....
There is NO.....

Por favor selecione o tipo de chave desejado:
   (1) RSA e RSA (padrão)
   (2) DSA e Elgamal
   (3) DSA (apenas assinatura)
   (4) RSA (apenas assinar)
  (14) Existing key from card
Sua opção? 1
```

Escolher 4096
```bash
RSA chaves podem ter o seu comprimento entre 1024 e 4096 bits.
Que tamanho de chave você quer? (3072) 4096
```

Escolher tempo, exemplo 1 ano
```bash
O tamanho de chave pedido é 4096 bits
Por favor especifique por quanto tempo a chave deve ser válida.
         0 = chave não expira
      <n>  = chave expira em n dias
      <n>w = chave expira em n semanas
      <n>m = chave expira em n meses
      <n>y = chave expira em n anos
A chave é valida por? (0) 1y
A chave expira em sex 06 jun 2077 06:05:12 -03
Está correto (s/N)? y
```

Preencher dados
```bash
Escolher nome e e-mail
Nome completo: Your Name
Endereço de correio eletrônico: yourEmail@gmail.com.com
Comentário: 
You are using the 'utf-8' character set.
Você selecionou este identificador de usuário:
    "Your Name <yourEmail@gmail.com.com>"

Muda (N)ome, (C)omentário, (E)ndereço ou (O)k/(S)air? o
Precisamos gerar muitos bytes aleatórios. É uma boa idéia realizar outra
atividade (digitar no teclado, mover o mouse, usar os discos) durante a
```



Listar chaves novamente
```bash
gpg --list-secret-key --keyid-form LONG
```

Exemplos de KEY_YOUR_GPG
```bash
sec   rsa4096/KEY_YOUR_GPG 2024-06-06 [SC] [expira: 2077-06-06]
```
Exportar uma public key

```bash
$ gpg --armor --export KEY_YOUR_GPG
```

Copy all text from your public key

```bash
-----BEGIN PGP PUBLIC KEY BLOCK-----
BLABLABLA
-----END PGP PUBLIC KEY BLOCK-----
```

Adicione a key no git

```bash
git config --global user.signinkey KEY_YOUR_GPG
```

Adicione a key no bash


```bash
nano ~/.bashrc 
# Adicione no final
export GPG_TTY=$(tty)
```

Diga para o git assinar os commits e tags por padrão

```bash
git config --global commit.gpgsign true
git config --global tag.gpgSign true
```

No github, vá em `configurações` e vá em `SSH and GPG keys` e crie uma nova chave

REINICIE SEU BASH, OU ABRA E FECHE

Se não estiver funcionando, o gpg pode estar off.

Agora faça commits, digite sua senha, a dependendo do lugar você pode salvar sua key.

-------------

# Adicionar outros e-mails

Editar a chave

```bash
gpg --edit-key KEY_YOUR_GPG
```

Adicionar id

```bash
gpg> adduid
Nome completo: TourNameSecondEmail
Endereço de correio eletrônico: newEmail@example.com
Comentário: 
Você selecionou este identificador de usuário:
    "TourNameSecondEmail <newEmail@example.com>"

Muda (N)ome, (C)omentário, (E)ndereço ou (O)k/(S)air? o
```

Selecionar o novo, que é o 2 nesse caso

```bash
gpg> uid 2
```

Confiar

```bash
gpg> trust
```

Confirmar

```
Por favor decida quanto você confia neste usuário para
verificar corretamente as chaves de outros usuários
(olhando em passaportes, checando impressões digitais
de outras fontes...)

  1 = Eu não sei ou nem direi
  2 = Eu NÃO confio
  3 = Eu tenho pouca confiança
  4 = Eu confio totalmente
  5 = Eu confio ao extremo
  m = voltar ao menu principal

Sua decisão? 5
Você quer realmente definir esta chave à confiança final? y
```

Salvar

```bash
gpg> save
```



