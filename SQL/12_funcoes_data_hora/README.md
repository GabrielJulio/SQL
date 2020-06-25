# Funções de Data e Hora

* No comando __SELECT__ há diversas funções que foram embutidas para facilitar o manuseio de alguns tipos dedados em determinadas condições.

    Estas funções são particularmente úteis a programadores, uma vez que conseguirão obter diretamente do banco de dados o tratamento a formatos ou resultados que dependeriam de algum algoritmo, seem ter que escrever código na linguagem fonte da aplicação para tais recursos.

    Algumas dstas funções são para se trabalharcom data e hora.
    
    *Estes comandos podem seer usados com base de dados mas não são presos a somente bases de dados.

* __CURDATE__

    Retorna a data atual no formato yyyy-mm-dd.
    ```sql
    SELECT CURDATE() AS 'Data Atual';
    ```

* __CURTIME__

    Retorna a hora atual no formato hh:mm:ss.
    ```sql
    SELECT CURTIME() AS 'Hora Atual';
    ```

* __CURRENT_TIMEDATE__

    Faz o mesmo que o __CURTIME__.
    ```sql
    SELECT CURTIME() AS 'Data Atual';
    ```

* __DATE_ADD(data, intervalo)__

    Adiciona um intervalo à data. O intervalo pod ser uma data seguida de um horário. O intervalo a ser somado pode ser em dias, dias e horas e minutos, dias e segundos, minutos e segundos e etc.
    ```sql
    SELECT DATE_ADD(CURDATE(), INTERVAL 3 DAY) AS 'Data de Vencimento';
    ```

* __DATE_SUB(data, intervalo)__

    Subtrai um intervalo de uma data. Assim como no __DATE_ADD__ o intervalo pode ser uma data seguida de um horário, O intervalo a ser somado pode ser em dias, dias e horas e minutos, dias e segundos, minutos e segundos e etc.
    ```sql
    SELECT DATE_SUB(CURDATE(), INTERVAL 7 DAY) AS 'Data de Matrícula';
    ```

* __DATEDIFF(expressao_1, expressao_2)__

    Retorna o valor da diferênça entre duas expressões.
    ```sql
    SELECT DATEDIFF(
        CURDATE(), DATE_SUB(CURDATE(), INTERVAL 1 MONTH)
    ) AS 'Dias em Atraso';
    ```

* __DATE_FORMAT(data, formato)__

    Formata um data no padrão especificado.
    ```sql
    SELECT DATE_FORMAT(CURDATE(), '%d/%m/%Y') AS 'Data Formatada';
    -- formatando a data para padrão brasileiro

    -------------------------------------------------------------------

    SET lc_time_names = 'pt_BR'; -- retornando nomes em português.
    SELECT DATE_FORMAT(CURDATE(), '%d/%m/%Y') AS 'Data Formatada e em Portugês';
    ```

* __DAYNAME(data)__

    Retorna o dia da semana da data especificada.
    ```sql
    SELECT DAYNAME() AS 'Dia da Semana';

    -------------------------------------------------------------------

    SET lc_time_names = 'pt_BR'; -- retornando nomes em português.
    SELECT DAYNAME() AS 'Dia da Semana em Portugês';
    ```

* __DAYOFMONTH(data)__

    Retorna o dia do mês da data especificada.
    ```sql
    SELECT DAYOFMONTH() AS 'Dia do Mês';

    -------------------------------------------------------------------

    SET lc_time_names = 'pt_BR';
    SELECT DAYOFMONTH() AS 'Dia do Mês em Portugês';
    ```


* __DAYOFWEEK(data)__

    Retorna o dia da semana da data especificada.
    ```sql
    SELECT DAYOFWEEK() AS 'Dia da Semana';
    ```
    *De Domingo - 1 até Sábado - 7.

* __DAYOFYEAR(data)__

    Retorna o dia do mês da data especificada.
    ```sql
    SELECT DAYOFYEAR() AS 'Dia do Ano';
    ```
    *Dia 1 até 365(ou 366 em ano bixesto)

* __FROM_DAYS(n)__

    Retorna a data real referente a um número em 'n' dias.

    ```sql
    SELECT FROM_DAYS(780500) AS 'Data Real';
    ```
    *Essa função só funciona somente com o calendário __Gregoriano__.

* __NOW__

    Retorna data e hora atual.
    ```sql
    SELECT NOW() AS 'Data e Hora Atual';

    -------------------------------------------------------------------

    SELECT DATE_FORMAT(NOW(), '%h:%m%s %d/%m/%Y') AS 'Hora e Data Atual';
    ```

* __CURRENT_TIMESTAMP__

    Faz o mesmo que a __NOW__.
    ```sql
    SELECT CURRENT_TIMESTAMP() AS 'Data e Hora Atual';
    ```

* __TIME(data)__

    Remove a data do argumento passado.
    ```sql
    SELECT TIME(CURRENT_TIMESTAMP()) AS 'Hora';
    ```

* __SEC_TO_TIME(segundos)__

    Converte segundos em horas/minutos/segundos.
    ```sql
    SELECT SEC_TO_TIME(2000) AS 'Tempo Real';
    ```

* __TIME_TO_SEC(tempo)__

    Converte tempo real em segundos.
    ```sql
    SELECT TIME_TO_SEC('00:32:44') AS 'Segundos';
    ```

* __HOUR(hora), MINUTE(hora), SECOND(hora)__

    Essas funções retornam a hora __HOUR(hora)__, minutos __MINUTE(hora)__ e segundos __SECOND(hora)__ de acordo com o atributo selecionado respectivo ao seu nome.

    ```sql
    SELECT
        HOUR('12:30:34') AS Hora, MINUTE('12:30:34') AS Minuto, SECOND('12:30:34') AS Segundo;
    ```

* __PERIOD_DIFF(periodo_1, perido_2)__

    Retorna o número de meses entre os dois períodos, que devem estar no formato AAMM ou AAAAMM.

    ```sql
    SELECT PERIOD_DIFF(201912, 201903) AS 'Meses Restantes';
    ```

* __TIME_DIFF(periodo_1, perido_2)__

    Retorna o número de horas entre os dois períodos de hora.

    ```sql
    SELECT TIME_DIFF('12:35:34', '12:30:46') AS 'Diferença de horas';
    ```

* __QUARTER(data)__

    Retorna o trimestre do ano da data informada.

    ```sql
    SELECT QUARTER('2019/12/01') AS 'Trimestre';
    ```

* __WEEK(data)__

    Retorna o número da semana da data informada.
    ```sql
    SELECT WEEK('2016/06/15') AS 'Semana do Ano';
    ```

* __WEEKDAY(data)__

    Retorna o dia da semana que inicia com segunda-feira para a data informada.
    ```sql
    SELECT WEEKDAY('2016/06/15') AS 'Dia da semana';
    ```

* __YEAR(data)__

    Retorna o ano da data informada.
    ```sql
    SELECT YEAR('2016/06/15') AS 'Ano';
    ```

* __MONTH(data)__

    Retorna o mês da data informada.
    ```sql
    SELECT MONTH('2016/06/15') AS 'Mês';
    ```

* __DAY(data)__

    Retorna o dia da data informada.
    ```sql
    SELECT DAY('2016/06/15') AS 'Dia';
    ```

### Anterior: [Agrupamento e Ordenação](https://github.com/GabrielJulio/bd/blob/master/SQL/11_agrupamento_ordenacao/README.md)

### [Sub Consultas](https://github.com/GabrielJulio/bd/blob/master/SQL/13_sub_consultas/README.md)