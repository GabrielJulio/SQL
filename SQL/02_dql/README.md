# DQL - Data Query Language

### DQL
1. __DQL__ é um subgrupo da linguagem __SQL__ e nos temos apenas 01 (um) comando <u>__SELECT__</u>.

    Exemplos:
    ```sql
    SELECT * FROM empresa;

    SELECT emp_id, emp_nome FROM empresa;
    ```
1. Também pode ser aplicado um __alias__ para o nome do campo ou nome da tabela.

    Exemplos:
    ```sql
    SELECT emp_nome AS empresa, emp.endereco AS 'endereço', fun_nome AS nome, fun_salario AS salario FROM funcionario;

    SELECT fun.emp_nome, emp.endereco, fun.fun_nome, fun.fun_salario FROM empresa AS emp, funcionario AS fun;
    ```

## Recomendação
- Escreva suas consultas __SQL__ em separando da seguinte forma para ficar mais fácil de visualizar, segundo exemplo do item 2 formatado.

    Exemplo:
    ```sql
    SELECT
        fun.emp_nome, emp.endereco, fun.fun_nome, fun.fun_salario
    FROM
        empresa AS emp, funcionario AS fun
    WHERE
        /* condição caso tenha
    ;
    ```