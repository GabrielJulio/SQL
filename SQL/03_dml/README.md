# DML - Data Manipulation Language

### DML
1. __DML__ esse subgrupo é com 03 (três) comandos: <u>__INSERT__</u>, <u>__UPDATE__</u> e <u>__DELETE__</u>.

    1. __INSERT__

        Exemplos:
        ```sql
        INSERT INTO tipo_produto (tp_descricao) VALUES ('Computador');

        /* note que a tabela tipo_produto tem como chave primária um
        campo chamado "tp_codigo", por ele ser chave primária e
        auto incremento logo será incremntado automaticamente. */

        INSERT INTO
            produto (pro_descricao, pro_preco, tp_codigo)
        VALUES
            ('Phantom Intel', 2500, 1);
        ```
    1. __UPDATE__

        Exemplos:
        ```sql
        UPDATE
            tipo_produto SET tp_descricao = 'Nobreak'
        WHERE
            tp_codigo = 2;

        UPDATE
            produto SET pro_descricao = 'Notebook', pro_preco = 2900
        WHERE
            pro_codigo = 2;
        ```

    1. __Delete__

        Exemplos:
        ```sql
        DELETE FROM
            produto
        WHERE
            pro_codigo = 3;
        ```

# JAMAIS... esqueça de filtrar quando fizer UPDATE ou DELETE !!!
    
- Exemplos:
```sql
    UPDATE
        produto SET preco = 10;
        
    DELETE FROM
        produto;
```