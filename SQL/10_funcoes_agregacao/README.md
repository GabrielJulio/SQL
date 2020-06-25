# Funções de Agregação


* É muito comum se desenvolver uma aplicação que necessite de informações resumidas, como quantas vendas foram feitas na semana, a maior venda do mês, vendedor com mais vendas.

    A  linguagem __SQL__ possui diversas funções nativas para esse fim, que podem ser usadas para agregar um conjunto de valores em um único resultado através de uma consulta
    
    Uma função de de agregação processa um conjunto de valores contidos em uma única coluna de uma tabela e retorna um únicovalor como resultado.
* __Max__

    Analiza todos os dados daquele campo da tabela e retorna o que têm o maior valor.
    ```sql
    SELECT MAX(preco_venda) FROM produtos;

    -------------------------------------------------------------------

    SELECT id_categoria, MAX(preco_venda)
    FROM produtos
    GROUP BY id_categoria;

    -------------------------------------------------------------------

    SELECT id_categoria, MAX(preco_venda)
    FROM produtos
    GROUP BY id_categoria
    HAVING MAX(pre_venda) > 3;
    ```
    *Quando usar uma função de agregação ao lado de outros campos sem as funções então deve-se obrigatoriamente fazer agrupamento.

    *O __HAVING__ funciona de forma semelhante ao __WHERE__, mas [e geralmente utilizada junto a funções de agregação equanto o __WHERE__ é utilizado com o __SELECT__.
* __Min__
    
    Analiza todos os dados daquele campo da tabela e retorna o que têm o menor valor.
    ```sql
    SELECT MIN(preco_venda)
    FROM produtos;
    ```
* __Sum__
    
    Soma todos os valores daquele campo da tabela e retorna o resultado.
    ```sql
    SELECT SUM(preco_venda)
    FROM produtos
    WHERE id_categoria = 1;
    ```
* __Avg__
    
    Analiza todos os valores daquele campo da tabela e retorna a média aritimética daquele campo.
    ```sql
    SELECT AVG(preco_venda)
    FROM produtos;
    ```
* __Round__
    
    Arredonda valores e também especifíca quantas casas decimais queremos que apareça no(s) resultado(s)
    ```sql
    SELECT ROUND(AVG(preco_venda), 2) -- apenas duas casas decimais aqui
    FROM produtos;
    ```
    
* __Count__
    
    Retorna a quantidade de linhas/resultados selecionados.

    \*Quando passamos o nome de uma coluna os valores __NULL__ serão ignorados, porém quando se utilizar do asterisco (*) todas as linhas serão contabilizadas
    ```sql
    SELECT COUNT(AVG(preco_venda)) -- apenas duas casas decimais aqui
    FROM produtos;
    ```

### Anterior: [Junção de tabelas](https://github.com/GabrielJulio/bd/blob/master/SQL/09_juncao_tabelas/README.md)

### Próximo: [Agrupamento e Ordenação](https://github.com/GabrielJulio/bd/blob/master/SQL/11_agrupamento_ordenacao/README.md)