# Junção de Tabelas

### DQL
* Em um banco de dados podemos ter uma  ou mais tabela relacionadas.
    É bem comum termos que elaborar consultas que recuperem dados de mais de uma tabela.
    
    Para criarmos esta seleção de dados devemos definir os critérios de agrupam,ento para fazer estees dados, esses critérios são chamados de **junções**.

    Uma junção de tabelas cria uma pseudo-tabela derivada de duas ou mais tabelas de acordo com as regras especificadas.

    ```sql
    CREATE DATABASE juncao;
    
    USE juncao;

    CREATE TABLE profissoes(
        id INT NOT NULL AUTO_INCREMENT,
        cargo VARCHAR(60) NOT NULL,
        PRIMARY KEY (id)
    );

    CREATE TABLE clientes(
        id INT NOT NULL AUTO_INCREMENT,
        nome VARCHAR(60) NOT NULL,
        data_nascimento DATE NOT NULL,
        telefone VARCHAR(10) NOT NULL,
        id_profissao int NOT NULL,
        PRIMARY KEY (id),
        /* a linha a seguir indicamos que o campo id_profisso 
        faz referencia a uma chave primaira de outra tabela,
        no caso o campo id da tabela profissoes */
        FOREIGN KEY (id_profissao) REFERENCES profissoes(id)
    );

    INSERT INTO profissoes (cargo) VALUES ('Suporte');
    INSERT INTO profissoes (cargo) VALUES ('Analista de Sistemas');
    INSERT INTO profissoes (cargo) VALUES ('Programador');
    INSERT INTO profissoes (cargo) VALUES ('Desenvolvedor');
    INSERT INTO profissoes (cargo) VALUES ('Gerente');


    -- OBS.: o formato usado para os campos DATE é yyyy-mm-dd
    INSERT INTO clientes (nome, data_nascimento, telefone, id_profissao)
    VALUES ('Samira Palos Teodoro', '1990-10-24', '92938-0959', 1);
    INSERT INTO clientes (nome, data_nascimento, telefone, id_profissao)
    VALUES ('Lais Cangueiro Tinoco', '1959-09-04', '91509-7389', 2);
    INSERT INTO clientes (nome, data_nascimento, telefone, id_profissao)
    VALUES ('Célio Furtado Nobre', '1942-10-20', '97621-1567', 3);
    INSERT INTO clientes (nome, data_nascimento, telefone, id_profissao)
    VALUES ('Fabrício Machado Campelo', '2013-03-02', '96230-9329', 4);
    INSERT INTO clientes (nome, data_nascimento, telefone, id_profissao)
    VALUES ('Morgana Neto Viegas', '2004-10-27', '96119-3750', 5);
    ```

* Junção Cartesiana: é a junção de duas tabelas que gera uma terceira com todos oselementos da primeira e segunda combinados.
    ```sql
    SELECT * FROM profissoes, clientes;
    /* note a forma como saem os resultados.
    estranho de visualizar assim não?
    vamos organizar um pouco */

    -------------------------------------------------------------------

    SELECT
        cli.id, cli.nome, cli.data_nascimento, cli.telefone, pro.cargo
    FROM
        clientes AS cli, profissoes AS pro
    WHERE
        cli.id_profissao = pro.id;
    -- melhor agora né?
    ```
* Junção Interna(_Inner Join_): é caracterizada por consulta que retorna apenas os dados que atendem as condições de junção, ou seja, as linhas da tabela que se relacionam com as linha de outras tabelas.

    Para isso utilizamos a cláusula __ON__ (que é parecida com a __WHERE__).
    
    ```sql
    SELECT
        cli.id, cli.nome, cli.data_nascimento, cli.telefone, pro.cargo
    FROM
        clientes AS cli INNER JOIN profissoes AS pro
    ON
        cli.id_profissao = pro.id;
    ```

* Junções Externas(_Outer Join_) é aquela quenão requer que os registros de uma tabela possuam registros equivalentes em outra tabela.

    Este tipo de junção se subdivide dependendo da tabela do qual admitiremos os registros que não possuem correspondêcia: a tabela da esquerda, a da direita ou ambas.
    
    * Junção Externa à Esquerda (_Left Outer Join_)

        O resultado desta consulta sempre contém todos os registros da tabela a esquerda (ou seja a primeira a ser mencionada na consulta), mesmo quando não exista registros correspondentes na tabela a direita.
        Mas como assim??

        Dessa forma esta consulta retorna todos os valores da tabela esquerda com os valores da tabela a direita correspondente, ou quando não há correspondência retorna valor __NULL__.
        ```sql
        SELECT *
        FROM clientes
        LEFT OUTER JOIN profissoes
        ON clientes.id_profissao = profissao.id;
        -- Legal o resultado, não é?
        ```
    * Junção Externa à Direita (_Right Outer Join_)

        O resultado desta consulta é o contrário da anterior, sempre contém todos os registros da tabela a direita (ou seja a segunda a ser mencionada na consulta), mesmo quando não exista registros correspondentes na tabela a esquerda.

        Dessa forma esta consulta retorna todos os valores da tabela direita com os valores da tabela a esquerda correspondente, ou quando não há correspondência também retorna valor __NULL__.
        ```sql
        SELECT *
        FROM clientes
        RIGHT OUTER JOIN profissoes
        ON clientes.id_profissao = profissao.id;
        -- Viu a mudançã? Show de Bola!!
        ```

    * Junção Externa (_Full Outer Join_)

        Esta consulta apresenta todos os dados das tabelas à esquerda e à direita mesmo que não possuam correspondência na outra tabela.

        A tabela combinada possuirá assim todos os registros de ambas as tabelas e apresentará os valores nulos para os registros sem correspondência.

        Essa consulta traz os dados de ambas as tabelas de acordo com suas correspondências e caso não tenha também retorna valor __NULL__.
        ```sql
        SELECT *
        FROM clientes
        FULL OUTER JOIN profissoes
        ON clientes.id_profissao = profissao.id;
        -- Sensacional, não é mesmo?

        -------------------------------------------------------------------

        /* O  MySQL não da suporte a essa função, nele você pode obter
        resultado similar juntando o LEFT com o RIGHT */
        SELECT *
        FROM clientes
        LEFT OUTER JOIN profissoes
        ON clientes.id_profissao = profissoes.id
        UNION -- aqui se faz a união das duas tabelas geradas
        SELECT *
        FROM clientes
        LEFT OUTER JOIN profissoes
        ON clientes.id_profissao = profissoes.id;
        ```

* Junção Cruzada(_Cross Join_): Essa consulta é usada quando queremos juntar duas ou mais tabelas por cruzamento, ou seja para cada linha de uma tabela queremos todos os dados da outra tabela ou vice-versa.

    E  qual a diferença dessa consulta para o __Full Outer Join__? Essa não retorna resultados com valor __NULL__.

    ```sql
    SELECT
        cli.id, cli.nome, cli.data_nascimento, cli.telefone, pro.cargo
    FROM
        clientes AS cli
    CROSS JOIN
        profissoes AS pro;
    ```

* Auto Junção(_Self Join_): esta consulta é uma auto injeção de uma tabela a si mesma.
    ```sql
    CREATE TABLE consumidores(
        id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
        nome VARCHAR(50) NOT NULL,
        contato VARCHAR(50) NOT NULL,
        endereco VARCHAR(100) NOT NULL,
        cidade VARCHAR(100) NOT NULL,
        cep VARCHAR(20) NOT NULL,
        pais VARCHAR(50) NOT NULL,
    );

    INSERT INTO consumidores (nome, contato, endereco, cidade, cep, pais)
    VALUES ('Kauã Melo', 'Bryce Moreno', 'Vila Mello Moraes Filho, 583', 'Salvador', '40352-230', 'Brasil');
    INSERT INTO consumidores (nome, contato, endereco, cidade, cep, pais)
    VALUES ('Luana Ferreira', 'Arthur Martins', 'Quadra QR 511 Conjunto 02 1996', 'Samambaia', '72313-702', 'Brasil');
    INSERT INTO consumidores (nome, contato, endereco, cidade, cep, pais)
    VALUES ('Frances Thomas', 'Kenneth Boswell', '2249 Glory Road', 'Nashville', '37201', 'Estados Unidos');

    -------------------------------------------------------------------

    SELECT
        conA.nome AS 'Consumidor 1', conB.nome AS 'Consumidor 2',
        conA.cidade
    FROM consumidor AS conA
    INNER JOIN consumidor AS conB
    ON conA.id <> conB.id -- os ID's diferentes
    AND conA.cidade = conB.cidade;
    ```
    *Os ID's são diferentes mas a cidade é a mesma.

* Junção Baseada em Comparador(_Equi Join_): é um tipo específico de junção baseada em comparador e utiliza apenas comparações de igualdade.
    ```sql
    SELECT *
    FROM clientes
    JOIN profissoes
    ON clientes.id_profissao = profissoes.id;
    ```

* Junção Natural(_Natural Join_): é um caso especial de _Equi Join_ o resultado dessa comparação é o conjunto de todas as combinações iguais em seus nomes de atributos comuns.

    Como assim? Se uma tabela tem um atributo "id" e você comparar ela com outra tabela que tambem tenha um atributo "id" a comparação retornará somente os valores desses campos quando eles tiverem valores iguais. E também só mostra esse campo uma vez.
    ```sql
    SELECT *
    FROM clientes
    NATURAL JOIN profissoes;
    ```

### Anterior: [Consultas em múltiplas tabelas](https://github.com/GabrielJulio/bd/blob/master/SQL/08_multiplas_tabelas/README.md)

### Próximo: [Funções de Agregação](https://github.com/GabrielJulio/bd/blob/master/SQL/10_funcoes_agregacao/README.md)