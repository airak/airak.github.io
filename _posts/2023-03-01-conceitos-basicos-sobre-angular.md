---
title: Conceitos básicos sobre Angular
date: 2023-03-06 19:48:00 -0300
categories: [Conceitos, Front-end]
tags: [angular, typescript, front-end, web]
render_with_liquid: false
img_path: /assets/img/posts/02_angular/
image:
  path: angular_header.png
  alt: Logo do angular com fundo espacial.
---

O Angular é um framework de desenvolvimento front-end, que utiliza HTML, CSS e TypeScript. Ele é um framework de código aberto e mantido pelo google, sendo um dos mais populares atualmente, sua primeira versão foi lançada em setembro de 2016.

Embora tenham nomes parecidos, Angular e AngularJS são frameworks diferentes, tendo apenas o nome em comum, já que durante o desenvolvimento da segunda versão do framework (conhecido hoje como Angular) foi realizada uma reescrita completa do framework.

O AngularJS foi lançado em 2010, ele utilizava como linguagem padrão o JavaScript e teve o seu [suporte descontinuado em janeiro de 2022](https://blog.angular.io/discontinued-long-term-support-for-angularjs-cc066b82e65a).

Nesta postagem faleremos sobre o Angular, no momento desta publicação a versão mais recente é a 15 e será ela que utilizaremos para a demonstração de funcionamento.

## Versionamento

O padrão de versionamento utilizado por ele é o SEMVER (Semantic Versioning), que é constituido por uma sequência de três números separados por pontos.

![Imagem ilustrativa sobre o versionamento do semver, explicando o que cada campo significa](semver02.png){: .shadow  w="600"}
_Padrão de versionamento do SEMVER_

* Major - É incrementado quando existem mudanças significativas, com potêncial de "quebrar" códigos que utilizam versões anteriores, como por ex. o lançamento de uma nova versão de determinada biblioteca, onde o nome ou assinatura de algumas de suas funções foi alterado. Sendo assim, para atualizar para uma nova major release é esperado que o desenvolvedor precise rodar scripts de atualização, refatorar código, fazer testes adicionais e estudar as novas APIs.
* Minor - Disponibilização de melhorias menores que não tem potencial para quebrar o código de quem já está utilizando aquela versão Major. É esperado que o desenvolvedor não precise de assistência para efetuar a atualização, mas você pode opcionalmente modificar a sua aplicação para utilizar os novos recursos que foram disponibilizados.
* Patch - Correções de bugs durante a release, assim como a Minor é esperado que o desenvolvedor não precise de assistência para a realização da atualização do patch.

De acordo com a documentação oficial a [frequência esperada da release](https://angular.io/guide/releases#release-frequency) é de:

* Major - Lançamento a cada 6 meses
* Minor - É esperado o incremento de 1 a 3 Minors em cada Major
* Patch - Frequência de expedição semanal

## Elementos básicos

Existem vários elementos básicos (building blocks) que podem ser bastante úteis durante o desenvolvimento de aplicações Angular, abaixo mostraremos os principais deles.

### Módulos

Os módulos são um conjunto de componentes, serviços e outros elementos que tenham alguma diretiva em comum. Ele é denotado pelo decorator `@ndModule`

Conforme o projeto for crescendo o módulo raiz pode ficar grande demais, desta forma é interessante a utilização de módulos locais/de funcionalidades (com funções específicas), estes módulos são conhecimentos como feature-modules.

Comando para criação de um módulo:

```console
ng g module [nome_modulo] --routing
```

<!-- Tem mais coisas nas minhas notas do curso -->

### Componentes

O componente é um bloco da aplicação Angular, contendo um arquivo de template (HTML), controle (ts) e o arquivo de estilização (css/scss). Ele é denotado pelo decorator `@Component`

Dentro do decorator Component, são listados:
* `selector`: O seletor é utilizado para "invocação" do componente dentro do HTML;
* `templateUrl`: O HTML utilizado para template do componente;
* `styleUrls`: O arquivo de estilização do componente.

Comando para criação de um componente:

```console
ng g component [nome_componente]
```

### Serviços

Os serviços normalmente são utilizados para conter o código responsável por um determinado propósito, como por exemplo a parte de consumo e envio de informações para as API (back-end), atualização do token de acesso, entre outras.

O decorator `Injectable` indica que a classe pode ser fornecida e injetada em outra classe.


Comando para criação de um serviço:

```console
ng g service [caminho\nome_servico]
```

### Data Binding

São uma forma de associar informações que estão no componente ao template e vice-versa.

Existem várias formas de se fazer isso, como:

* Do Componente para o Template
    * Interpolação: `{{ valor }}`
    * Property Binding: `[propriedade]="valor"`
* Do Template para o Componente
    * Escutar eventos do template: `(evento)="handler"`
    * Two-way data bind (usado em formulários para manter os dois atualizados ao mesmo tempo): `[(ngModel)]="propriedade"`

Para encontrar outras formas de se utilizar Data Binding [clique aqui](https://angular.io/guide/binding-syntax#binding-types-and-targets).

## Estrutura de diretórios

Existe uma estrutura comum de arquivos em projetos Angular, a seguir falaremos de alguns que já vem na configuração inicial do projeto.

![Visão da estrutura inicial de um projeto Angular](estrutura_inicial_prj_angular.png){: .shadow  w="300"}
_Estrutura inicial de um projeto Angular_

* .gitignore - Especifica os arquivos que não devem subir para o git.
* node_modules - Diretório que contém os pacotes npm da aplicação (package.json)
* src - Diretório de código fonte da aplicação. Dentro dela teremos:
    * app - Contem os arquivos de componentes do projeto.
    * assets - Pasta que contém imagens e outros tipos de arquivos.
    * index.html - A página HTML princial que é exibida quando alguém visita o seu site.
    * style.css - Arquivo de estilização global da aplicação.
* package.json - Contém os nomes e as versões dos pacotes instalados.
* angular.json - Contém as informações do projeto e build de produção, como nome do projeto, config de onde encontrar os arquivos fontes, config de testes, etc.

Para encontrar mais detalhes sobre os arquivos e diretórios mencionados acima e muitos outros [clique aqui](https://angular.io/guide/file-structure#workspace-configuration-files).

## Mão na massa

1. Instalação do angular

    O primeiro passo para fazer a instalação do Angular, é ter o Node.js instalado. Caso ainda não tenha, acesse o [site do Node.js](https://nodejs.org/en/) e faça o download da última versão destinada ao seu sistema operacional.

    Com o Node.js será possível instalar o Angular CLI, que é a interface de linha de comando do Angular, para realizar a sua instalação execute o comando abaixo no terminal do seu computador:

    ```console
    npm install -g @angular/cli
    ```
    Após a instalação poderemos interagir com o Angular CLI através do comando `ng`.

2. Inicialização do projeto

    Para criar seu primeiro projeto com Angular basta executar o comando abaixo no terminal, ele criará um projeto com a mesma estrutura de diretório mencionada no tópico anterior deste texto.

    ```console
    ng new meu-primeiro-app
    cd meu-primeiro-app
    ```

    Para executar a aplicação Angular no seu ambiente de desenvolvimento é preciso utilizar o ng serve, por padrão ele irá criar um servidor web local que disponibilizará o acesso a sua aplicação através da porta `4200` do `localhost`, caso você utilize o parâmetro `-o` ele irá abrir a aplicação em uma nova aba do navegador após a sua compilação.

    ```console
    ng serve -o
    ```
    Após a execução do `ng serve` você deverá ser capaz de visualizar a seguinte página:

    ![Captura de tela do projeto sendo acessado dentro do navegador Chrome](meu_primeiro_projeto.png){: .shadow  w="800"}
_Visualizaçao do "Meu primeiro projeto" no navegador_


## Referências

1. [Treinamento de Angular da Loiane](https://loiane.training/continuar-curso/angular)
2. [Documentação do Angular](https://angular.io/)
3. [O que é o Angular e para que serve?](https://www.treinaweb.com.br/blog/o-que-e-o-angular-e-para-que-serve)
4. [Versionamento Semântico (SemVer): uma breve introdução](https://www.alura.com.br/artigos/versionamento-semantico-breve-introducao)
5. [O que é TypeScript? [Guia para iniciantes]](https://tecnoblog.net/responde/o-que-e-typescript-guia-para-iniciantes/)
