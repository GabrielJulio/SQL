# Sub Consultas

* De forma geral grande parte das consultas realizadas em um banco de dados podem ser resolvidas de forma simples, porém nem sempre isso é possível ou desejável.
    Existem casos onde é necessário aumentar a complexidade para se obter os resultados ou desejável para que se tenha um resultado mais limpo e de melhor leitura.

    Uma __subconsulta__ nada mais ]e do que uma instrução __SELECT__ dentro de outro __SELECT__ que retorna algumas colunas específicas que são usadas em algumas funções como __INSERT__, __UPDATE__ E __DELETE__.

    __Banco base__
    ```sql
    CREATE DATABASE subconsulta;
    USE subconsulta;

    CREATE TABLE escritorios(
        id INT NOT NULL AUTO_INCREMENT,
        pais VARCHAR(30) NOT NULL,
        PRIMARY KEY (id)
    );

    CREATE TABLE funcionarios(
        id INT NOT NULL AUTO_INCREMENT,
        nome VARCHAR(20) NOT NULL,
        sobrenome VARCHAR(20) NOT NULL,
        id_escritorio INT NOT NULL,
        PRIMARY KEY (id),
        FOREIGN KEY (id_escritorio) REFERENCES escritorios(id)
    );

    CREATE TABLE pagamentos(
        id INT NOT NULL AUTO_INCREMENT,
        id_funcionario INT NOT NULL,
        salario DECIMAL(8, 2) NOT NULL
        data DATE NOT NULL,
        PRIMARY KEY (id),
        FOREIGN KEY (id_funcionario) REFERENCES funcionarios(id)
    );

    INSERT INTO escritorios (pais) VALUES ('Brasil');
    INSERT INTO escritorios (pais) VALUES ('Estados Unidos');
    INSERT INTO escritorios (pais) VALUES ('Alemanha');
    INSERT INTO escritorios (pais) VALUES ('França');

    INSERT INTO funcionarios (nome, sobrenome, id_escritorio)
    VALUES ('Pedro', 'Sousa', 1),
    INSERT INTO funcionarios (nome, sobrenome, id_escritorio)
    VALUES ('Sandra', 'Rubin', 2),
    INSERT INTO funcionarios (nome, sobrenome, id_escritorio)
    VALUES ('Mikail', 'Schumer', 3),
    INSERT INTO funcionarios (nome, sobrenome, id_escritorio)
    VALUES ('Oliver', 'Gloçan', 4);

    INSERT INTO pagamentos (id_funcionario, salario, data)
    VALUES (1, '5347.55', '2020-06-25');
    INSERT INTO pagamentos (id_funcionario, salario, data)
    VALUES (2, '9458.46', '2020-06-25');
    INSERT INTO pagamentos (id_funcionario, salario, data)
    VALUES (3, '4669.67', '2020-06-25');
    INSERT INTO pagamentos (id_funcionario, salario, data)
    VALUES (4, '2770.32', '2020-06-25');

    -------------------------------------------------------------------
    
    SELECT nome, sobrenome
    FROM funcionarios
    WHERE id_escritorio
    IN (SELECT id
        FROM escritorios
        WHERE pais = 'Brasil');
    ```
    *Ocorrem primeiro as __subconsultas__ e retorna um conjunto de resultados, depois é executado a consulta externa em cima dos resultados das suas subconsultas

    ```sql
    SELECT
        fun.nome, fun.sobrenome, esc.pais, pag.salario
    FROM
        pagamentos AS pag, escritorios AS esc, pagamentos AS pag
    WHERE
        fun.id_escritorio = esc.id AND
        fun.id = pag.id_funcionario AND
        salario = (SELECT MAX(salario)
                   FROM pagamentos);
    -- Começando a ficar bonito, não é?

    -------------------------------------------------------------------

    SELECT
        fun.nome, fun.sobrenome, esc.pais, pag.salario
    FROM
        pagamentos AS pag, escritorios AS esc, pagamentos AS pag
    WHERE
        fun.id = esc.id AND
        fun.id = pag.id_funcionario AND
        salario < (SELECT AVG(salario)
                   FROM pagamentos);
    ```

### Anterior: [Funções de Data e Hora](https://github.com/GabrielJulio/bd/blob/master/SQL/12_funcoes_data_hora/README.md)