---
title: Tutorial - Git
author: Matheus
date: 2023-02-20 18:30:00 -0300
categories: [Blogging, Tutorial]
tags: [git]
render_with_liquid: false
img_path: /assets/img/posts/
---

## O que é o git?
Git provavelmente é o sistema de versionamento de código distribuído mais popular no mundo, ele foi desenvolvido em 2005 por ninguém mais e ninguém menos que o grande mestre jedi Linux Torvalds quando o serviço que ele utilizava para isso se tornou pago.
Como um bom sistema de versionamento de código, o git permite que várias pessoas trabalhem no mesmo projeto, editando simultaneamente os mesmos arquivos,  sem o risco de que uma sobrescreva o que a outra fez. Além de permitir que as alterações realizadas possam ser desfeitas.

## Como o git funciona?
O git funciona através da arquitetura de branches, que são ramificações do código principal. Nestas branches o desenvolvedor pode realizar alterações sem se preocupar em gerar impactos no código principal durante o processo de desenvolvimento. Após o término do desenvolvimento ele realiza um merge da branch criada com a branch principal (normalmente chamada de main ou master).

## Exemplo de utilização
Hoje em dia é possível utilizar o git de várias formas diferentes, seja através do uso de linhas de comando, através de alguns softwares como sourcetree, github desktop e até mesmo através de algumas IDEs que contam com integração com o git, como por ex. o Visual Studio.
Além disso, conforme mencionado anteriormente a branch principal do seu repositório pode possuir vários nomes diferentes, mas os mais comuns são master (nomenclatura antigo) e main (nova nomenclatura). Para a exemplificação a seguir, iremos considerar a utilização através da linha de comando e com a branch principal sendo nomeada como main.

1. Inicialmente é necessário realizar a criação de um repositório git na plataforma de sua preferência (github, gitlab, bitbucket, etc). Caso o repositório já exista isto não será necessário.
    Com o repositório já criado, é preciso fazer um clone deste repositório para o seu ambiente local.
    ```console
    $ git clone url
    ```
2. Quando você realiza o clone de um repositório, por padrão você estará utilizando a branch principal, neste caso a main, desta forma, para seguir com o desenvolvimento é recomendado que se crie uma nova branch.
    ```console
    $ git checkout -b nome_da_branch
    ```
    Com o comando acima você irá criar e começar a utilizar a nova branch.
    Com a branch criada você poderá iniciar o desenvolvimento, é importante que ao longo do desenvolvimento você realize commits a cada marco atingido. Os commits podem ser considerados como a publicação daquela alteração realizada dentro da branch que você está utilizando.
3. Para realizar um commit através da linha de comando você precisa de três comandos:
    ```console
    $ git add .
    $ git commit -m "mensagem descrevendo o que está sendo publicado por aquele commit"
    $ git push
    ```
4. Após o término do desenvolvimento daquela funcionalidade e a realização de todos os commits você deverá realizar a junção das alterações realizadas na branch de desenvolvimento com a branch principal.
    ```console
    $ git merge origin/main –no-ff
    ```

## Git e Github são a mesma coisa?

Embora sejam bem relacionados, o Git e o Github não são a mesma coisa. Git é o sistema de versionamento de código, enquanto o Github é como se fosse uma rede social de desenvolvedores, onde você pode criar seus repositórios (público ou privados) e contribuir com inúmeros projetos open source que estão dentro da plataforma.

![Uma postagem no reddit onde um cara pergunta qual é a diferença entre o git e o github e um outro responde falando que é igual a diferença do porn e do pornhub](difference_between_git_and_github.jpg){: .shadow  w="300"}
_Qual é a diferença entre o git e o github?_

Assim como o Github existem outras plataformas de gerenciamento de repositório baseados no git, como o Gitlab e o Bitbucket, cada um com seus prós e contras.

## Conclusão
Algumas pessoas até tentam realizar o gerenciamento manual de versões e alterações com a utilização de ferramentas como dropbox, pendrives e arquivos zips, mas isso é inviável. Desta forma, os sistemas de gerenciamento de repositórios se destacam devido as facilidades e seguranças que eles podem fornecer ao longo do desenvolvimento de nossos projetos, sejam em projetos pessoais, ou principalmente aqueles que envolvem mais de uma pessoa.

É extremamente improvável que um desenvolvedor não utilize alguma dessas ferramentas em ambientes profissionais ou em algum momento de sua vida, por isso quanto antes tiver contato e aprender a utilizá-las da melhor forma, melhor será.

## Referências

1. [Uma breve história do git](https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Uma-Breve-Hist%C3%B3ria-do-Git)
2. [O Criador do Linux: Conheça Linus Torvalds (A Historia de Linus Torvalds)](https://ilustradev.com.br/o-criador-do-linux-conheca-linus-torvalds/)
3. [Git e Github: o que são, como configurar e primeiros passos](https://www.alura.com.br/artigos/o-que-e-git-github)
