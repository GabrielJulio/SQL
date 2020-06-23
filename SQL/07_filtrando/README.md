# Filtrando consultas com WHERE

### DQL
1. __WHERE__
     
    Buscando pelo registro com codigo igual a 1.
    ```sql
        SELECT
            *
        FROM
            tipo_produto
        WHERE
            tp_codigo = 1;
    ```
    Buscando pelo registro com descricao seja exatamente 'Computador'.
    ```sql
        SELECT
            *
        FROM
            tipo_produto
        WHERE
            tp_descricao = 'Computador';
    ```
    Buscando pelo registro com descricao que comece por 'Comp'.
    ```sql
        SELECT
            *
        FROM
            tipo_produto
        WHERE
            tp_descricao LIKE 'Comp%';
    ```
    Buscando pelo registro com descricao que tenha por 'omp' em qualquer lugar.
    ```sql
        SELECT
            *
        FROM
            tipo_produto
        WHERE
            tp_descricao LIKE '%omp%';
    ```
    Buscando pelo produto com preco menor 200.
    ```sql
        SELECT
            *
        FROM
            produto
        WHERE
            pro_preco < 200;
    ```
    Buscando pelo registros ativos (registro com soft delete é 1).
    ```sql
        SELECT
            *
        FROM
            produto
        WHERE
            pro_deletado = 0;
    ```

### Anterior: [DTL - Data Transaction Language](https://github.com/GabrielJulio/bd/blob/master/SQL/06_dtl/README.md)

### Próximo: _Em Breve_