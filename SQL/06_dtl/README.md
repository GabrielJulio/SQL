# DTL - Data Transaction Language

### DTL
1. __DTL__ esse subgrupo contém 03 (três) comandos: <u>__BEGIN__</u>, <u>__COMMIT__</u> e <u>__ROLLBACK__</u>.

    *. __BEGIN__
        <br/> Usado para marcar o começo de uma transação que pode ser completada ou não.

    *. __COMMIT__
        <br/> Usado para finalizar uma transação.

    *. __ROLLBACK__
        <br/> Usado para descartar mudanças nos dados realizadas desde último __COMMIT__, ou seja a transação atual não pode ter sido finalizada ainda.

    Exemplos:
    ```sql
    CREATE TABLE produto(
        pro_codigo      INT PRIMARY KEY,
        pro_descricao   VARCHAR(50));


    BEGIN TRANSACTION; -- inicia a transação
        INSERT INTO
            produto
        VALUES ('Super PC');
        INSERT INTO
            produto
        VALUES ('Casas Bahia PC');
    COMMIT; -- termina a transação e grava os dados

    BEGIN TRANSACTION; -- inicia a transação
        INSERT INTO
            produto
        VALUES ('Rodolfo');
    ROLLBACK; -- todas as alterações feitas foram desfeitas
    COMMIT; -- esta linha não é lida e os dados não são salvos
    ```