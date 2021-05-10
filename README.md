# Básico

### Configurações 

    git config --global user.name "Gabriel Gregório"  
    git config --global user.email "gabriel.gregorio.1@outlook.com"   
    git config --global core.editor code    

### Ver uma configuração
    git config user.email


### Ver uma lista de todas as definições
    git config --list

# Criando o repositório

### Criação
    git init
    git status

### Estágios de um arquivo
TA INCOMPLETO

| Estágio | Descrição |
|---------|-----------|
| Untracked files | Arquivo não adicionado |
| Stage | Arquivo adicionado e preparado para o commit |
| Not Staged | Não preparado para o commit |
| commit | Criar um snapshot, uma versão |


# Outros
### Subindo um arquivo
    git commit -m "Primeiro commit"

### Ver o histórico e branchs unidas
    git log

### ?? Mostra cada commit e relações de branchs com tags??
    git log --decorate

### Filtrar por um autor
    git log --author='Kalia'

### Mensagem de todos os commits
    git shortlog

### Quantidade de commits de cada autor
    git shortlog -sn

### Grafico geral com merges
    git log --graph

### Ver as mudanças de um commit ENVIADO
    git show de99d4eda910dc834f414d8e59a5573a6e1cd21e

### Ver mudanças antes de commitar
    git diff

### Ver apenas o arquivo que foi modificado
    git diff --name-only

### Adiciona e já commita um arquivo existente
    git commit -am "Edit Readme"




# Reversão
### Quebrou o sistema, mas os arquivos não foram adicionados ainda, como reverter?
    git checkout readme.md

#### Tirar o arquivo do stage (add)
    git reset HEAD

### Depois do commit quebrou
> pega um hash antes do commit bugado

    git reset --soft 55ca76b8464fd8013861a69c768eb5a350e79455

### voltar antes do stage (add)
    git reset --mixed 3b9bfc5feb84249255df03c8406dfb12c38ffaea

### Destruir o Commit por completo
> Altera o histórico e, portanto, para evitar conflitos não é interessante usa-lo
    git reset --hard 3b9bfc5feb84249255df03c8406dfb12c38ffaea

# Configs do repositório remoto
### Gerar chave ssh
https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh    

    ssh-keygen -t ed25519 -C "seuemail@email.com"

#### Adicionar origem para subir
    git remote add origin git@github.com:gabrielogregorio/teste.git

### Remover origin do repositório
    git remote rm origin

### Subir repositório
    git push -u origin main


# infos de clone e FORK
* Clone: Não consegue enviar modificações para o autor original. Se for projeto seu, ok, pode enviar, mas de terceiros não!

* Fork: Pega um projeto que não é seu e faz uma cópia para você. No caso é para contribuição.


# Branchs
> c1 - c2 - c3(Master) - c4(branch)
> Pode modificar os arquivos sem modificar no master
> Facilmente desligável
> Menos conflitos nos brenchs individuais

### Criando um brach
    git checkout -b bteste

### vendo os branchs
    git branch

### Acessar um brach
    git checkout master

### Apagar um branch
    git branch -D bteste

# Como unir o branch com o master
### Merge
Cria um commit novo, junta o master com o brach secundário.


**Pros**  
* Merge é uma operação não destrutiva, ele não estraga o histórico

**Contra**
* Precisa de um novo commit somente para juntar ambos.
* Deixa o histórico feio.

    git merge bmerge



### Rebase.
Move o commit para a frente, modificando o histórico das brancs. Coloca na frente da fila

**pros**  
* Evita commit extras
* Histórico linear

**Contras**
* Perde a ordem cronologica
* muda o histórico

    git rebase brebase


REBASE é BEM MELHOR POIS NAO POLUI O HISTORICO. SO USE O MERGE CASO PRECISE DO HISTORICO PERFEITO

------------

# Gitignore
### gitignore   
https://git-scm.com/docs/gitignore

### Templates   
https://github.com/github/gitignore


# Outros
### git stash
Guarda informações que foram MODIFICADOS, MAS NÃO ADICIONADAS em um arquivo que eu posso chamar depois
    git stash

### Aplica as modificações guardadas novamente
    git stash apply

### Lista de todas as stash
git stash list

### Limpa todo o histórico
git stash clear

### Atalhos no git
    git config --global alias.s status


### Renomeando a branch principal
    git branch --move master main
    git push -u origin main
    git push origin --delete master

### Trabalhando com as tags.
Acabei o front, tag de fim de front
    git tag -a 1.0.0 -m "REAME FINALIZADO"
    git push origin main --tags


-------------

# Outras reversões
Quando eu tiver mais tempo quero ver o que aconteceu, mas sem perder meu código.
### Revert
    git revert 16110104a33763e5d109932edb1afaa43f21b0a3

# Apagar no repositório remoto
### Apagar tags no local
    git tag -d 1.0.1

### Apagar no remoto
    git push origin :1.0.0
