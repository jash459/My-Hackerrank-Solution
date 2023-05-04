### Basic Select
1. Type of Triangle 

Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

- Equilateral: It's a triangle with  sides of equal length.
- Isosceles: It's a triangle with  sides of equal length.
- Scalene: It's a triangle with  sides of differing lengths.
- Not A Triangle: The given values of A, B, and C don't form a triangle.
Input Format

The TRIANGLES table is described as follows:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12887/1443815827-cbfc1ca12b-2.png "This is a sample image.")

Each row in the table denotes the lengths of each of a triangle's three sides.

Sample Input

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12887/1443815629-ac2a843fb7-1.png "This is a sample image.")

Sample Output

Isosceles
Equilateral
Scalene
Not A Triangle
Explanation

Values in the tuple (20, 20, 23)  form an Isosceles triangle, because A=B.
Values in the tuple (20, 20, 20) form an Equilateral triangle, because A=B=C. Values in the tuple (20,21,22) form a Scalene triangle, because A!= B!= C.
Values in the tuple  cannot form a triangle because the combined value of sides A and B is not larger than that of side C.

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/what-type-of-triangle/problem?isFullScreen=true).

```
Query : Select 
CASE
when A + B <= C or A + C <= B or B + C <= A then "Not A Triangle"
when A = B and B = C then "Equilateral"
when A = B or A = C or B = C then "Isosceles"
else "Scalene"
end as triangle_sides
from TRIANGLES;
```


2. The PADS
   
  Generate the following two result sets:
  1. Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
  2. Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:

  ```
  There are a total of [occupation_count] [occupation]s.
  ```

  where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.

Note: There will be at least two entries in the table for each type of occupation.

Input Format

The OCCUPATIONS table is described as follows:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12889/1443816414-2a465532e7-1.png "This is a sample image.")

Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.

Sample Input

An OCCUPATIONS table that contains the following records:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12889/1443816608-0b4d01d157-2.png "This is a sample image.")

Sample Output

Ashely(P)
Christeen(P)
Jane(A)
Jenny(D)
Julia(A)
Ketty(P)
Maria(A)
Meera(S)
Priya(S)
Samantha(D)
There are a total of 2 doctors.
There are a total of 2 singers.
There are a total of 3 actors.
There are a total of 3 professors.

Explanation

The results of the first query are formatted to the problem description's specifications.
The results of the second query are ascendingly ordered first by number of names corresponding to each profession (2 <= 2 <= 3 <= 3), and then alphabetically by profession (doctors <= singer, and actor <= professor).

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/the-pads/problem?isFullScreen=true).


```
Query : select concat(name,'(',substring(Occupation,1,1),')') as Name 
from occupations 
order by Name;
Select concat ('There are a total of ', count(occupation),' ', lower(occupation),'s.') as totals
from occupations
group by occupation
order by totals;
```


3. Ocupations
   
   Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output column headers should be Doctor, Professor, Singer, and Actor, respectively.

Note: Print NULL when there are no more names corresponding to an occupation.

Input Format

The OCCUPATIONS table is described as follows:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12889/1443816414-2a465532e7-1.png "This is a sample image.")

Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.

Sample Input

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12890/1443817648-1b2b8add45-2.png "This is a sample image.")

Sample Output

Jenny    Ashley     Meera  Jane
Samantha Christeen  Priya  Julia
NULL     Ketty      NULL 

Explanation

The first column is an alphabetically ordered list of Doctor names.
The second column is an alphabetically ordered list of Professor names.
The third column is an alphabetically ordered list of Singer names.
The fourth column is an alphabetically ordered list of Actor names.
The empty cell data for columns with less than the maximum number of names per occupation (in this case, the Professor and Actor columns) are filled with NULL values.

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/occupations/problem?isFullScreen=true).

```
Query : set @d=0, @p=0, @s=0, @a=0;

select min(Doctor), min(Professor), min(Singer), min(Actor)
from(
  select case 
            when Occupation='Doctor' then (@d:=@d+1)
            when Occupation='Professor' then (@p:=@p+1)
            when Occupation='Singer' then (@s:=@s+1)
            when Occupation='Actor' then (@a:=@a+1) 
            end as Row,
        case when Occupation='Doctor' then Name end as Doctor,
        case when Occupation='Professor' then Name end as Professor,
        case when Occupation='Singer' then Name end as Singer,
        case when Occupation='Actor' then Name end as Actor
  from OCCUPATIONS
  order by Name
) as temp
group by Row;
```


4. Binary Tree Nodes
   
   You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12888/1443818507-5095ab9853-1.png "This is a sample image.")

Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:

- Root: If node is root node.
- Leaf: If node is leaf node.
- Inner: If node is neither root nor leaf node.
Sample Input

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12888/1443818467-30644673f6-2.png "This is a sample image.")

Sample Output

1 Leaf
2 Inner
3 Leaf
5 Root
6 Leaf
8 Inner
9 Leaf

Explanation

The Binary Tree below illustrates the sample:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12888/1443773633-f9e6fd314e-simply_sql_bst.png "This is a sample image.")

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/binary-search-tree-1/problem?isFullScreen=true).

```
Query : SELECT BT.N,
CASE
    WHEN BT.P IS NULL THEN 'Root'
    WHEN EXISTS (SELECT B.P FROM BST B WHERE B.P = BT.N) THEN 'Inner'        
    ELSE 'Leaf'
END
FROM BST AS BT 
ORDER BY BT.N;
```


5. New Companies
   
   Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19505/1458531031-249df3ae87-ScreenShot2016-03-21at8.59.56AM.png "This is a sample image.")

Given the table schemas below, write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. Order your output by ascending company_code.

Note:

The tables may contain duplicate records.
The company_code is string, so the sorting should not be numeric. For example, if the company_codes are C_1, C_2, and C_10, then the ascending company_codes will be C_1, C_10, and C_2.

Input Format

The following tables contain company data:

- Company: The company_code is the code of the company and founder is the founder of the company.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19505/1458531125-deb0a57ae1-ScreenShot2016-03-21at8.50.04AM.png "This is a sample image.")

- Lead_Manager: The lead_manager_code is the code of the lead manager, and the company_code is the code of the working company.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19505/1458534960-2c6d764e3c-ScreenShot2016-03-21at8.50.12AM.png "This is a sample image.")

- Senior_Manager: The senior_manager_code is the code of the senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19505/1458534973-6548194998-ScreenShot2016-03-21at8.50.21AM.png "This is a sample image.")

- Manager: The manager_code is the code of the manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19505/1458534988-7fc0af46ce-ScreenShot2016-03-21at8.50.29AM.png "This is a sample image.")

- Employee: The employee_code is the code of the employee, the manager_code is the code of its manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19505/1458535002-d47f63cbb4-ScreenShot2016-03-21at8.50.41AM.png "This is a sample image.")

Sample Input

Company Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19505/1458535049-2a207c44b3-ScreenShot2016-03-21at8.50.52AM.png "This is a sample image.")

Lead_Manager Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19505/1458535073-919107f639-ScreenShot2016-03-21at8.51.03AM.png "This is a sample image.")

Senior_Manager Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19505/1458535111-b1c48335b3-ScreenShot2016-03-21at8.51.15AM.png "This is a sample image.")

Manager Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19505/1458535122-888f4bf340-ScreenShot2016-03-21at8.51.26AM.png "This is a sample image.")

Employee Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19505/1458535134-878767e0d9-ScreenShot2016-03-21at8.51.52AM.png "This is a sample image.")

Sample Output

C1 Monika 1 2 1 2
C2 Samantha 1 1 2 2
Explanation

In company C1, the only lead manager is LM1. There are two senior managers, SM1 and SM2, under LM1. There is one manager, M1, under senior manager SM1. There are two employees, E1 and E2, under manager M1.

In company C2, the only lead manager is LM2. There is one senior manager, SM3, under LM2. There are two managers, M2 and M3, under senior manager SM3. There is one employee, E3, under manager M2, and another employee, E4, under manager, M3.

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/japanese-cities-name/problem?isFullScreen=true).

```
Query : SELECT c.company_code,c.founder,
count(distinct lm.lead_manager_code),
count(distinct sm.senior_manager_code),
count(distinct m.manager_code), 
count(distinct e.employee_code)
FROM Company c, Lead_Manager lm, Senior_Manager sm, Manager m, Employee e
WHERE
c.company_code=lm.company_code AND
lm.lead_manager_code=sm.lead_manager_code AND
sm.senior_manager_code=m.senior_manager_code AND
m.manager_code=e.manager_code
GROUP BY c.company_code,c.founder
ORDER BY c.company_code **ASC**;
```


