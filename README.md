## Gitflow   s
### Configurações   
No Windows o Gitflow já vem instalado com o git, mas no Linux/MacOs, é preciso instalar o git e o gitflow

    sudo apt-get install git-flow

Então é preciso inicializar o gitflow no repositório, use o comando abaixo

    git flow init

O comando abaixo permite verificar as branchs, agora deveremos ter a branch main e a develop. A main é sagrada e devemos nos aventurar na branch develop.

    git branch

Para trocar de branch precisamos executar o comando abaixo (Mas não mexa na Main por enquanto)

    git checkout main


Para enviar a branch develop para o GitHub devemos rodar o seguinte comando

    git push -u origin develop

### Features

A partir da branch develop, podemos criar as features da aplicação, com o gitflow podemos usar o seguinte comando

    git flow feature start feature_gitflow

Agora faça todos os commits necessários para a criação da feature


Para finalizar a feature use o seguinte comando

    git flow feature finish feature_gitflow

### Bugfix

Para a correção de bugs usamos a branch bugfix

    git flow bugfix start bugfix_bug_y


Para finalizar a branch use o seguinte comando

    git flow bugfix finish bugfix_bug_y

### Releases

Quando a develop tiver features o suficiente para uma nova versão, iremos gerar um release

Criando uma release seguindo o versionamento semântico

    git flow release start 0.1.0

Faça os testes, e quando estiver tudo ok é só finalizar a branch e fazer o push no repositório MAIN

    git flow release finish '0.1.0' -m "Versão com novos recursos"


Use o comando abaixo para verificar a releases.

    git tag


### Hotfix

Para correção de bugs direto em produção usamos o seguinte comando (Use o versionamento Semântico)
    
    git flow hotfix start x.x.x

Após feito a correção, é preciso rodar o comando abaixo para finalizar a branch

    git flow hotfix finish  x.x.x -m "Correçao no bug x"

------------

## Versionamento Semântico    

As versões devem ser numeradas com números de 0 a 9, sendo no seguinte formato
```text
Major, Minor, Patch // => 1.0.0
```

| Item | Descrição |
|------|-----------|
| Major | Cada versão nova informa funcionalidade e códigos incompatíveis com os anteriores |
| Minor | Informa novas funcionalidades, sem incompatibilidade com versões anteriores |
| Patch | Indica correção de bugs, porém, sem quebra de compatibilidade |
| Pré-release | Versão ainda instável |


--------------------

## Git & GitHub

### Configurações    

    git config --global user.name "Gabriel Gregório"  
    git config --global user.email "gabriel.gregorio.1@outlook.com"   
    git config --global core.editor code    

### Ver uma configuração

    git config user.email


### Ver uma lista de todas as definições

    git config --list

----------------

## Inicializando o git

### Criação  

    git init
    git status

### Estágios de um arquivo    
| Estágio | Descrição |
|---------|-----------|
| Untracked files | Arquivo não adicionado |
| Stage | Arquivo adicionado e preparado para o commit |
| Not Staged | Não preparado para o commit |
| commit | Criar um snapshot, uma versão |

Subindo um arquivo

    git commit -m "Primeiro commit"

Ver o histórico e branchs unidas

    git log

Mostra cada commit e relações de branchs com tags??

    git log --decorate

Filtrar por um autor

    git log --author='Kalia'

Mensagem de todos os commits

    git shortlog

Quantidade de commits de cada autor

    git shortlog -sn

Grafico geral com merges

    git log --graph

Ver as mudanças de um commit ENVIADO

    git show de99d4eda910dc834f414d8e59a5573a6e1cd21e


Ver mudanças antes de commitar

    git diff

Ver apenas o arquivo que foi modificado

    git diff --name-only

Adiciona e já commita um arquivo existente

    git commit -am "Edit Readme"


Reverter alterações em um arquivo

    git checkout readme.md

Tirar o arquivo do stage (add)

    git reset HEAD
 
Depois do commit quebrar   
> pega um hash antes do commit bugado

    git reset --soft 55ca76b8464fd8013861a69c768eb5a350e79455

voltar antes do stage (add)

    git reset --mixed 3b9bfc5feb84249255df03c8406dfb12c38ffaea

Destruir o Commit por completo

> Altera o histórico e, portanto, para evitar conflitos não é interessante usá-lo

    git reset --hard 3b9bfc5feb84249255df03c8406dfb12c38ffaea

---------------

## Gerar chave ssh

https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh    

    ssh-keygen -t ed25519 -C "seuemail@email.com"

Adicionar origem para subir

    git remote add origin git@github.com:gabrielogregorio/teste.git

Remover origin do repositório

    git remote rm origin

Subir repositório

    git push -u origin main


## Informações de clone e FORK
* Clone: Não consegue enviar modificações para o autor original. Se for projeto seu, ok, pode enviar, mas de terceiros não!

* Fork: Pega um projeto que não é seu e faz uma cópia para você. No caso é para contribuição.

---------------

## Branchs
> c1 - c2 - c3(Master) - c4(branch)
> Pode modificar os arquivos sem modificar no master
> Facilmente desligada
> Menos conflitos nos brenchs individuais

Criando um brach

    git checkout -b bteste

vendo os branchs

    git branch

Acessar um brach

    git checkout master

Apagar um branch

    git branch -D bteste

------------

## Como unir o branch com o master
### Merge
O merge cria um commit novo, junta o master com o brach secundário.


**Pros**  
* Merge é uma operação não destrutiva, ele não estraga o histórico

**Contra**   
* Precisa de um novo commit somente para juntar ambos.
* Deixa o histórico feio.

    git merge bmerge

### Rebase   
O Rebase move o commit para a frente, modificando o histórico das brancs. Coloca na frente da fila

**pros**    
* Evita commit extras
* Histórico linear

**Contras**     
* Perde a ordem cronologica
* muda o histórico

    git rebase brebase


REBASE é BEM MELHOR POIS NAO POLUI O HISTORICO. SO USE O MERGE CASO PRECISE DO HISTORICO DETALHADO

------------

## Links úteis

[gitignore](https://git-scm.com/docs/gitignore)

[gitignore Templates](https://github.com/github/gitignore)

---------------

## Outros comandos git
Guarda informações que foram MODIFICADOS, MAS NÃO ADICIONADAS em um arquivo que eu posso chamar depois
    git stash


Aplica as modificações guardadas novamente

    git stash apply

Lista de todas as stash

    git stash list

Limpa todo o histórico

    git stash clear

Atalhos no git

    git config --global alias.s status


Renomeando a branch principal

    git branch --move master main
    git push -u origin main
    git push origin --delete master

Trabalhando com as tags. Acabei o front, tag de fim de front

    git tag -a 1.0.0 -m "REAME FINALIZADO"
    git push origin main --tags



## Reversões
Código quebrou, quero salvar a versão atual e voltar na antiga, depois volto nessa versão e verifico o problema, como fazer?

Usando o git Revert

    git revert 16110104a33763e5d109932edb1afaa43f21b0a3

## Outros
### Apagar tags no local

    git tag -d 1.0.1

### Apagar no remoto

    git push origin :1.0.0
