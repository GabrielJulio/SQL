# Agrupamento e Ordenação


* Durante o desenvolvimento de uma aplicação é comum ser necessário agrupar e/ou ordenar os resultados para uma melhor visualização.

    __Banco base__
    ```sql
    CREATE DATABASE agrupamento;
    USE agrupamento;

    CREATE TABLE tipos(
        id INT NOT NULL AUTO_INCREMENT,
        nome VARCHAR(60) NOT NULL,
        PRIMARY KEY (id)
    );

    CREATE TABLE fabricantes(
        id INT NOT NULL AUTO_INCREMENT,
        nome VARCHAR(60) NOT NULL,
        PRIMARY KEY (id)
    );

    CREATE TABLE produtos(
        id INT NOT NULL AUTO_INCREMENT,
        nome VARCHAR(60) NOT NULL,
        id_fabricante INT NOT NULL,
        quantidade INT NOT NULL,
        id_tipo INT NOT NULL,

        PRIMARY KEY (id),
        FOREIGN KEY (id_fabricante) REFERENCES fabricantes(id),
        FOREIGN KEY (id_tipo) REFERENCES id_tipo(id),
    );

    INSERT INTO tipos (nome) VALUES ('Console');
    INSERT INTO tipos (nome) VALUES ('Notebook');
    INSERT INTO tipos (nome) VALUES ('Celular');
    INSERT INTO tipos (nome) VALUES ('Smartphone');
    INSERT INTO tipos (nome) VALUES ('Sofá');
    INSERT INTO tipos (nome) VALUES ('Armário');
    INSERT INTO tipos (nome) VALUES ('Refrigerador');

    INSERT INTO fabricantes (nome) VALUES ('Sony');
    INSERT INTO fabricantes (nome) VALUES ('Dell');
    INSERT INTO fabricantes (nome) VALUES ('Microsoft');
    INSERT INTO fabricantes (nome) VALUES ('Samsung');
    INSERT INTO fabricantes (nome) VALUES ('Apple');
    INSERT INTO fabricantes (nome) VALUES ('Beline');
    INSERT INTO fabricantes (nome) VALUES ('Magno');
    INSERT INTO fabricantes (nome) VALUES ('CCE');
    INSERT INTO fabricantes (nome) VALUES ('Nintendo');

    INSERT INTO produtos (nome, id_fabricante, quantidade, id_tipo)
    VALUES ('PlayStation 5', 1, 100, 1);
    INSERT INTO produtos (nome, id_fabricante, quantidade, id_tipo)
    VALUES ('I5 12GB RAM 500Gb HD', 2, 50, 2);
    INSERT INTO produtos (nome, id_fabricante, quantidade, id_tipo)
    VALUES ('Xbox One S 1Tb HD', 3, 350, 1);
    INSERT INTO produtos (nome, id_fabricante, quantidade, id_tipo)
    VALUES ('GT-I6220 Quad Band', 4, 300,31);
    INSERT INTO produtos (nome, id_fabricante, quantidade, id_tipo)
    VALUES ('iPhone 4 32Gb', 5, 50, 4);
    INSERT INTO produtos (nome, id_fabricante, quantidade, id_tipo)
    VALUES ('PlayStation 2', 1, 100, 1);
    INSERT INTO produtos (nome, id_fabricante, quantidade, id_tipo)
    VALUES ('Sofá Estofado', 6, 200, 5);
    INSERT INTO produtos (nome, id_fabricante, quantidade, id_tipo)
    VALUES ('Armário de Serviço', 7, 50, 6);
    INSERT INTO produtos (nome, id_fabricante, quantidade, id_tipo)
    VALUES ('Refrigerador 420L', 8, 200, 7);
    INSERT INTO produtos (nome, id_fabricante, quantidade, id_tipo)
    VALUES ('Switch 500Gb', 8, 250, 1);
    ```

* __Group By__

    Utilizamos a cláusula __GROUP BY__ para fazermos agrupar elementos do mesmo tipo.
    ```sql
    SELECT
        tip.nome AS Tipo, SUM(pro.quantidade) AS 'Quantidade em Estoque'
    FROM
        tipos AS tip, produtos AS pro
    WHERE
        tip.id = pro.id_tipo
    GROUP BY tip.nome;

    -------------------------------------------------------------------

    SELECT
        fab.nome AS Fabricante, SUM(pro.quantidade) AS 'Quantidade em Estoque'
    FROM
        fabricantes AS fab, produtos AS pro,
    WHERE
        fab.id = pro.id_fabricante
    GROUP BY fab.nome;

    -------------------------------------------------------------------

    SELECT
        tip AS Tipo, fab.nome AS Fabricante, SUM(pro.quantidade) AS 'Quantidade em Estoque'
    FROM
        tipos AS tip, fabricantes AS fab, produtos AS pro
    WHERE
        tip.id = pro.id_tipo AND
        fab.id = pro.id_fabricante
    GROUP BY
        tip.nome, fab.nome;

    -------------------------------------------------------------------

    SELECT
        tip.nome AS Tipo, fab.nome AS Fabricante, SUM(pro.quantidade) AS 'Quantidade em Estoque'
    FROM
        tipos AS tip, fabricantes AS fab, produtos AS pro
    WHERE
        tip.id = pro.id_tipo AND
        fab.id = pro.id_fabricante
    GROUP BY
        tip.nome, fab.nome
    HAVING SUM(pro.quantidade) > 200;

    -------------------------------------------------------------------

    SELECT tip.nome AS Tipo
    FROM produtos AS pro, tipos AS tip
    WHERE tip.id = pro.id_tipo;
    -- Veja o resultado deste aqui e pare para pensar
    
    -- Agora adicione GROUP BY tip.nome e rode novamente
    ```

* __Order By__

    Utilizamos a cláusula __ORDER BY__ para fazermos a ordenação dos resultados, seja texto ou numérico. A ordenação pode ser fita de forma __ASC__ (ascendente) ou __DESC__ (descente).

    Por padrão a ordenação é ASC caso não seja definida ordenação.
    ```sql
    SELECT
        id, nome, id_tipo, id_fabricante, quantidade
    FROM produtos

    -------------------------------------------------------------------

    SELECT id, nome, id_tipo, id_fabricante, quantidade
    FROM produtos
    ORDER BY id DESC;

    -------------------------------------------------------------------

    SELECT id, nome, id_tipo, id_fabricante, quantidade
    FROM produtos
    ORDER BY quantidade DESC;
    ```

### Anterior: [Junção de tabelas](https://github.com/GabrielJulio/bd/blob/master/SQL/09_juncao_tabelas/README.md)

### Próximo: [Funções de Data e Hora](https://github.com/GabrielJulio/bd/blob/master/SQL/12_funcoes_data_hora/README.md)