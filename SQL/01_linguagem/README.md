# Linguagem SQL

### SQL
1. __SQL__ é a linguagem padrão dos bancos de dados relacionais e ela se divide em 5 subgrupos:
    * __DQL__ - Data Query Language (_Linguagem de consulta de dados_)
        * Comandos para fazer consulta de dados.
    * __DML__ - Data Manipulation Language (_Linguagem de manipulação de dados_)
        * Comandos para manipulação de dados como inserir, atualizar e excluir dados.
    * __DDL__ - Data Definition Language (_Linguagem de definição de dados_)
        * Comandos que estão relacionados a definição dos dados como criação de bancos de dados, criação de tabelas, criação de campos nas tabelas.
    * __DCL__ - Data Control Language (_Linguagem de controle de dados_)
        * Comandos que estão relacionados ao controle de acesso aos dado como permissões de acesso a tabela, forma de visualização de dados de usuário. 
    * __DTL__ - Data Transaction Language (_Linguagem de transação de dados_)
        * Comandos relacionados as transações como início ou finalização de uma transação

1. Cada subgrupo **SQL** possui comandos próprios de execução e ao executar esses comandos sempre teremos:
    1. O resultado da execução do comando.
    1. Uma mensagem de sucesso ou falha.

## Recomendação
- Escreva os códigos __SQL__ em letras maiúsculas e as demais palavras (como tabelas, campos, etc) em minúsculo, para facilitar a leitura do seus comandos (esse é o padrão utilizado no mercado).
<br/>Exemplo:
    ```sql
    CREATE TABLE funcionario(
    fun_id       INT PRIMARY KEY NOT NULL,
    fun_nome     TEXT    NOT NULL,
    fun_idade    INT     NOT NULL,
    fun_endereco CHAR(50),
    fun_salario  REAL
    );
    ```

### Próximo: [DQL - Data Query Language](https://github.com/GabrielJulio/bd/blob/master/SQL/02_dql/README.md)