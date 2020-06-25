# DDL - Data Definition Language

### DDL
1. __DDL__ esse subgrupo contém 03 (três) comandos: <u>__CREATE__</u>, <u>__ALTER__</u> e <u>__DROP__</u>.

    * __CREATE__
        <br/>Usado para criar um banco de dados, tabela e outros objetos de um banco de dados.

        Exemplos:
        ```sql
        CREATE DATABASE financeiro;

        -------------------------------------------------------------------

        CREATE TABLE produto(
            pro_codigo      INT PRIMARY KEY,
            pro_descricao   VARCHAR(50)
        );
        ```
    * __ALTER__
        <br/>Usado para alterar a estrutura de tabela ou outro objeto de um banco de dados.

        Exemplos:
        ```sql
        ALTER TABLE
            produto
        ADD
            peso DECIMAL(5,2);
        ```

    * __Drop__
        <br/>Usado para apagar um banco de dados, tabela e outros objetos de um banco de dados.

        Exemplos:
        ```sql
        DROP DATABASE financeiro;

        -------------------------------------------------------------------

        DROP TABLE produto;
        ```

<b>Cuidado:</b> usar __DROP__ em um __banco de dados__ ou em uma __tabela__ que contenham dados, esses dados também serão apagados.

### Anterior: [DML - Data Manipulation Language](https://github.com/GabrielJulio/bd/blob/master/SQL/03_dml/README.md)
### Próximo: [DCL - Data Control Language](https://github.com/GabrielJulio/bd/blob/master/SQL/05_dcl/README.md)