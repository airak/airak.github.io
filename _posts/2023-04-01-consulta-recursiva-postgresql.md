---
title: Consultas recursivas em PostgreSQL
date: 2023-03-09 18:30:00 -0300
categories: [Tópicos avançados, Banco de dados]
tags: [banco de dados, postgreSQL, recursividade]
render_with_liquid: false
img_path: /assets/img/posts/03_postgresql_q_rec/
---

Imagine que você possua uma tabela que possua um relacionamento (FK) consigo mesma e precise extrair algum relatório disso. Existem várias formas de se fazer isso, a maneira convencional seria realizando várias consultas ao banco de dados pegando em cada uma dessas requisições a informação de um registro.

Neste artigo abordaremos a criação de consultas recursivas em um banco de dados PostgreSQL, desta forma seremos capazes de extrair as infomações necessárias para a geração do relatório realizando apenas uma consulta ao bando de dados. Este recurso encontra-se disponível desde a versão 8.4 do PostgreSQL.

## Sintaxe

```sql
WITH RECURSIVE tabela_auxiliar_consulta AS(
    <consulta_nao_recursiva>
    UNION [ALL]
    <consulta_recursiva>
) <consulta_final>;
```

* `tabela_auxiliar_consulta` - Tabela temporária que armazena os dados obtidos através da recursão.
* `consulta_nao_recursiva` - Retorna os dados base da consulta recursiva.
* `consulta_recursiva` - Ela terá os seus resultados unidos ao da consulta não recursiva, por isso elas devem retornar as mesmas informações, mesmo que não sejam necessariamente iguais. A consulta recursiva sempre fará referência a própria recursão através da tabela_auxiliar_consulta.
* `consulta_final` - Consulta que fará o retorno dos dados utilizando a tabela_auxiliar_consulta.

### Ordem de execução

![Imagem ilustrando a recursividade através de uma pintura que aparece dentro dela própria várias vezes](recursao.jpg){: .shadow  w="600"}

O PostgreSQL executa a consulta recursiva da seguinte forma:

1. Executa a consulta não recursivo para criar o conjunto de resultados base (R0).
2. Executa a consulta recursiva com Ri como entrada para retornar o conjunto de resultados Ri+1 como saída.
3. Repete a etapa 2 até que um conjunto vazio seja retornado. (verificação de rescisão)
4. Retorna o conjunto de resultados final que é um UNION ou UNION ALL do conjunto de resultados R0, R1, … Rn

> **_Nota:_**  Ao utilizar "Union" ao invés de "Union all" você acrescentará apenas elementos que ainda não foram adicionados na tabela_auxiliar_consulta, ou seja, já é um primeiro tratamento para possíveis loops, existem outras formas de tratamento, como [configurar um nível máximo de profundidade da consulta](https://stackoverflow.com/questions/51025607/prevent-infinite-loop-in-recursive-query-in-postgresql).

## Exemplo

Para exemplificar utilizaremos o seguinte cenário:

A empresa Skynet Consulta Recursiva, possui uma estrutura hierárquica onde cada funcionário possui um líder direto, a gerente Ana, deseja saber o nome de todos os funcionários subordinados da sua estrutura. Para fornecer esses nomes para a Ana implementaremos uma consulta recursiva que percorrerá a tabela de funcionários da empresa.

![Diagrama contendo a hierarquia da empresa do cenário de teste](diagrama.png){: .shadow  w="400"}_Diagrama de funcionários subordinados a Ana_

### Criação das tabelas

```sql
CREATE TABLE funcionario (
  id INTEGER NOT NULL PRIMARY KEY,
  nome VARCHAR(30),
  id_funcionario_superior INTEGER REFERENCES funcionario(id)
);

INSERT INTO funcionario (id, nome, id_funcionario_superior) VALUES (1, 'Ana Vitória', NULL);
INSERT INTO funcionario (id, nome, id_funcionario_superior) VALUES (2, 'Luiz Fernando', 1);
INSERT INTO funcionario (id, nome, id_funcionario_superior) VALUES (3, 'Maria Luiza', 1);
INSERT INTO funcionario (id, nome, id_funcionario_superior) VALUES (4, 'Laura Novaes', 2);
INSERT INTO funcionario (id, nome, id_funcionario_superior) VALUES (5, 'Nathan Ramos', 2);
INSERT INTO funcionario (id, nome, id_funcionario_superior) VALUES (6, 'Otávio da Rocha', 3);
```

### Consultas

Primeiro será executado a consulta não recursiva que retorna o id e o nome da Ana Vitória, essas informações são armazenadas na tabela temporária `subordinados`.
```sql
SELECT id, nome
FROM funcionario
WHERE nome = 'Ana Vitória';
```

Em seguida será executada a consulta recursiva, trazendo os funcionários que tem a Ana como superior (id_funcionario_superior).
```sql
-- Demonstração da consulta recursiva em sua primeira execução
SELECT id, nome
FROM funcionario
WHERE id_funcionario_superior = 1; --esse é o id da Ana
```
Essas informações também serão armazenadas na tabela temporária de subordinados. Para cada linha dessa tabela a consulta recursiva é executada novamente, até que nenhum dado seja retornado.

No final todas as informações estarão disponíveis na tabela de subordinados e a consulta final será executada. A consulta completa pode ser vista abaixo.

```sql
WITH RECURSIVE subordinados AS(
    SELECT id, nome
    FROM funcionario
    WHERE nome = 'Ana Vitória'

    UNION ALL

    SELECT funcionario.id, funcionario.nome
    FROM funcionario
    JOIN subordinados ON funcionario.id_funcionario_superior = subordinados.id
) SELECT nome
  FROM subordinados;
```

## Resultado

````
 num. linha  |    nome
-------------+-----------------
           1 | Ana Vitória
           2 | Luiz Fernando
           3 | Maria Luiza
           4 | Laura Novaes
           5 | Nathan Ramos
           6 | Otávio da Rocha
````

No resultado apresentado a Ana está inclusa, para mostrar apenas o nome dos funcionários que são subordinados a ela, basta adicionar uma cláusula na consulta final que a ignore, conforme mostrado abaixo.

```sql
WITH RECURSIVE subordinados AS(
    SELECT id, nome
    FROM funcionario
    WHERE nome = 'Ana Vitória'

    UNION ALL

    SELECT funcionario.id, funcionario.nome
    FROM funcionario
    JOIN subordinados ON funcionario.id_funcionario_superior = subordinados.id
) SELECT nome
  FROM subordinados
  WHERE nome <> 'Ana Vitória';
```

## Referências

1. [Learn PostgreSQL Recursive Query By Example](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-recursive-query/)
2. [Linguagem SQL: Consultas Recursivas](https://paca.ime.usp.br/pluginfile.php/76637/mod_resource/content/3/mac439_aula16.pdf)
