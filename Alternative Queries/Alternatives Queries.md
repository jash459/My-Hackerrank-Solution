### Alternative Queries
1. Draw The Triangle 1

P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):

```
 * * * * *
 * * * * 
 * * * 
 * *
 *
```

Write a query to print the pattern P(20).

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/draw-the-triangle-1/problem?isFullScreen=true).

```
Query : SELECT RPAD('*', (21-LEVEL)*2, ' *')
FROM DUAL CONNECT BY LEVEL <= 20;
```


2. Draw The Triangle 1
   
  P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):



Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/placements/problem?isFullScreen=true).

```
 * 
 * * 
 * * * 
 * * * * 
 * * * * *
 ```

 Write a query to print the pattern P(20).

```
Query : SELECT RPAD('*', 2 * LEVEL - 1, ' *')
FROM DUAL CONNECT BY LEVEL <= 20;
```

3. Print Prime Number
   
  Write a query to print all prime numbers less than or equal to 1000. Print your result on a single line, and use the ampersand (&) character as your separator (instead of a space).

For example, the output for all prime numbers <= 10 would be:

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/print-prime-numbers/problem?isFullScreen=true).

```
Query : WITH THOUSAND AS
  (SELECT *
   FROM
     (SELECT LEVEL LVL
      FROM DUAL CONNECT BY LEVEL <= 1000)
   WHERE LVL > 1)
SELECT LISTAGG(T1.LVL, '&') WITHIN GROUP(ORDER BY T1.LVL)
FROM THOUSAND T1
WHERE T1.LVL <=
    (SELECT COUNT(DISTINCT T2.LVL) + 2
     FROM THOUSAND T2
     WHERE T2.LVL < T1.LVL
       AND MOD(T1.LVL, T2.LVL) > 0);
```

