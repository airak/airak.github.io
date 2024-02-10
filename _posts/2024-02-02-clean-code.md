---
title: Código Limpo (Clean Code)
date: 2024-02-02 12:00:00 -0300
categories: [Conceitos, Boas práticas]
tags: [clean code, uncle bob, boas práticas]
render_with_liquid: false
img_path: /assets/img/posts/clean_code/
image:
  path: bob_5.jpeg
  alt: 
---

> Tornar seu código legível é tão importante quanto torná-lo executável.

<!-- ![Imagem de uma pessoa limpando uma tela com códigos utilizando produtos de limpeza](clean_code.png){: .shadow  w="600"} -->

Código limpo se refere a um estilo de escrita de código de programação que enfatiza a legibilidade, manutenibilidade e clareza do código-fonte. Um código limpo é fácil de entender, seguir e modificar, o que é fundamental para o desenvolvimento de software eficiente e sustentável. O conceito de código limpo foi popularizado por Robert C. Martin em seu livro "Clean Code: A Handbook of Agile Software Craftsmanship".

## Importância do código limpo

Um código limpo pode agregar uma série de vantagens ao processo de desenvolvimento de software, incluindo:

1. Legibilidade e Compreensão
2. Facilidade de manutenção
3. Redução de erros
5. Reutilização
6. Testabilidade
7. Redução de Custos a Longo Prazo:


#A importância do código limpo no desenvolvimento de software não pode ser subestimada, pois afeta diversos aspectos do ciclo de vida do software e contribui para a qualidade, eficiência e sustentabilidade de um projeto. Aqui estão algumas das razões pelas quais o código limpo é crucial:

## Características e princípios



### 1. Nomes significativos

O nome de uma variável, função ou classe deve responder a todas as grandes questões. Ele deve lhe dizer porque existe, o que faz e como é usado. Se um nome requer um comentários, então ele não revela seu propósito.

### 2. Funções

Implemente funções pequenas, onde cada uma possua responsabilidade única, funções grandes e complexas possuem baixa manutenabilidade e legibilidade.
Quando uma função parece precisar de mais de dois ou três parâmetros, é provável que alguns deles podem ser colocados em uma classe própria.

### 3. Comentários

Códigos mudam e evoluem, enquanto os comentários nem sempre.

> O uso adequado de comentários é compensar nosso fracasso em nos expressar no código. Devemos usá-los apenas porque nem sempre encontramos uma forma de nos expressar sem eles, mas seu uso não é motivo para comemoração.

O seu código deve ser auto-explicativo, desta forma, utilize comentários apenas para explicar o porquê de algumas decisões ou para documentar partes do código que sejam menos óbvias.

### 4. Não seja redundante

 Não repita o mesmo código em vários lugares. Em vez disso, crie funções ou classes reutilizáveis para evitar duplicação.

### 5. Regra do escoteiro

Deixe o código sempre mais limpo do que você o encontrou.

### 6. Testes limpos

Escreva testes unitários para garantir que seu código funcione conforme o esperado e possa ser facilmente validado durante o desenvolvimento e manutenção, afinal um código só é considerado limpo após ser validado através de testes.

Testes limpos seguem cinco regras que formam o acrônimo em inglês F.I.R.S.T.:

1. Rapidez (Fast) - Os testes devem ser rápidos, possibilitando a sua execução sempre que possível.
2. Independência (Independent) - Você deve ser capaz de executar os testes de forma independente e na ordem que desejar. Quando eles dependem uns dos outros, se o primeiro falhar irá causar um efeito dominó de falhas, dividultando a análise dos problemas.
3. Repetitividade (Repeatable) - Os testes devem ser possíveis de serem executados em qualquer ambiente.
4. Autovalidação (Self-Validating) - A saída dos testes deve ser true ou false para que a falha não seja subjetiva.
5. Pontualidade (Timely) - Os testes precisam ser escritos em tempo hábil e de preferência antes do código de produção.



## Referências

- Livro Clean Code
- [Clean Code - Guia e Exemplos](https://balta.io/blog/clean-code)
