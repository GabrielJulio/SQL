# Consultas em Múltiplas Tabelas

### DQL
* As vezes precisamos consultar valores/registros que estáo em mais de uma tabela, então....

    Considere que temos duas tabelas relacionadas "tipo_produto" e "produto" precisamos buscar 4 campos:
    ```
    - código do produto             (produto)
    - descrição do produto          (produto)
    - preço do produto              (produto)
    - descrição do tipo de produto  (tipo_produto)
    ```
    ```sql
    SELECT
        pro.codigo AS 'Código', pro.descricao AS 'Descrição',
        pro.preco AS 'Preço', tp.descricao AS 'Tipo de produto'
    FROM
        produto AS pro, tipo_produto AS tp
    WHERE
        pro.tp_codigo = tp.codigo;
        /* Note que filtramos para aparecer somente os "produtos" que tem o
        "código do tipo de produto" igual ao "código" da tabela "tipo
        de produto". */
    ```
    PS: Você sempre irá irá usar as chaves primárias e estrangeiras para relacionar tabelas, independente da quantidade de relacionamentos daquela entidade.
    
### Anterior: [Filtrando consultas com WHERE](https://github.com/GabrielJulio/bd/blob/master/SQL/07_filtrando/README.md)

### Próximo: _Em Breve_