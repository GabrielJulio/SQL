# DCL - Data Control Language

### DCL
1. __DCL__ Esse subgrupo é utilizado para controlar aspectos de autorização de dados e licenças de usuários para controlar quem tem acesso para manipular dados dentro do banco de dados e possui 02 (dois) comandos: <u>__GRANT__</u> e <u>__REVOKE__</u>.

    * __GRANT__
        <br/> Usado para autorizar um usuário ou setar operações  no banco de dados.

        Exemplo:
        ```sql
            GRANT SELECT ON
                produtos TO atendente;
            /* dando permissao para usuario atendente poder consultar
            os dados da tabela produtos */
        ```
    * __REVOKE__
        <br/> Usado para remover ou restringir a capacidade de um usuário de executar operações.

        Exemplo:
        ```sql
        REVOKE CREATE TABLE FROM
                cliente, atendente, gerente;
            /* restringindo a criação de tabelas do usuarios listados */
        ```

### Anteriror: [DDL - Data Definition Language](https://github.com/GabrielJulio/bd/blob/master/SQL/04_ddl/README.md)
### Próximo: [DTL - Data Transaction Language](https://github.com/GabrielJulio/bd/blob/master/SQL/06_dtl/README.md)