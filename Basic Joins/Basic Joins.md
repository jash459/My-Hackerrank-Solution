### Basic Select
1. Population Census

Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

Input Format

The CITY and COUNTRY tables are described as follows:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg "This is a sample image.")

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg "This is a sample image.")

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/asian-population/problem?isFullScreen=true).

```
Query : select sum(city.population) from country left join city on country.code = city.countrycode where country.continent = 'Asia';
```


2. African Cities
   
   Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

Input Format

The CITY and COUNTRY tables are described as follows:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg "This is a sample image.")

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg "This is a sample image.")

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/african-cities/problem?isFullScreen=true).

```
Query : select city.name from city join country on city.countrycode = country.code where country.continent = 'Africa';
```


3. Averge population of each continent
   
   Given the CITY and COUNTRY tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

Input Format

The CITY and COUNTRY tables are described as follows:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg "This is a sample image.")

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg "This is a sample image.")

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/average-population-of-each-continent/problem?isFullScreen=true).

```
Query : select country.continent, floor(avg(city.population)) from country join city on city.countrycode = country.code group by country.continent;

```


4. The Report 
   
   You are given two tables: Students and Grades. Students contains three columns ID, Name and Marks.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12891/1443818166-a5c852caa0-1.png "This is a sample image.")

Grades contains the following data:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12891/1443818137-69b76d805c-2.png "This is a sample image.")

Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

Write a query to help Eve.

Sample Input    

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12891/1443818093-b79f376ec1-3.png "This is a sample image.")

Sample Output

Maria 10 99
Jane 9 81
Julia 9 88 
Scarlet 8 78
NULL 7 63
NULL 7 68

Note

Print "NULL"  as the name if the grade is less than 8.

Explanation

Consider the following table with the grades assigned to the students:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12891/1443818026-0b3af8db30-4.png "This is a sample image.")

So, the following students got 8, 9 or 10 grades:

- Maria (grade 10)
- Jane (grade 9)
- Julia (grade 9)
- Scarlet (grade 8)

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/japanese-cities-attributes/problem?isFullScreen=true).

```
SELECT CASE
         WHEN G.grade > 7 THEN S.name
         ELSE NULL
       end AS names,
       G.grade,
       S.marks
FROM   students S
       JOIN grades G
         ON S.marks BETWEEN G.min_mark AND G.max_mark
ORDER  BY G.grade DESC,
          names ASC,
          S.marks ASC; 
```


5. Top Competitors
   
   Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.

The CITY table is described as follows:

Input Format

The following tables contain contest data:

- Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker. 

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19504/1458526776-67667350b4-ScreenShot2016-03-21at7.45.59AM.png "This is a sample image.")

- Difficulty: The difficult_level is the level of difficulty of the challenge, and score is the score of the challenge for the difficulty level.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19504/1458526915-57eb75d9a2-ScreenShot2016-03-21at7.46.09AM.png "This is a sample image.")

- Challenges: The challenge_id is the id of the challenge, the hacker_id is the id of the hacker who created the challenge, and difficulty_level is the level of difficulty of the challenge

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19504/1458527032-f9ca650442-ScreenShot2016-03-21at7.46.17AM.png "This is a sample image.")

- Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge that the submission belongs to, and score is the score of the submission

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19504/1458527077-298f8e922a-ScreenShot2016-03-21at7.46.29AM.png "This is a sample image.")

Sample Input

- Hackers Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19504/1458527241-6922b4ad87-ScreenShot2016-03-21at7.47.02AM.png "This is a sample image.")

- Difficulty Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19504/1458527265-7ad6852a13-ScreenShot2016-03-21at7.46.50AM.png "This is a sample image.")

- Challenges Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19504/1458527285-01e95eb6ec-ScreenShot2016-03-21at7.46.40AM.png "This is a sample image.")

- Submissions Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19504/1458527812-479a74b99f-ScreenShot2016-03-21at8.06.05AM.png "This is a sample image.")

Sample Output

90411 Joe
Explanation

Hacker 86870 got a score of 30 for challenge 71055 with a difficulty level of 2, so 86870 earned a full score for this challenge.

Hacker 90411 got a score of 30 for challenge 71055 with a difficulty level of 2, so 90411 earned a full score for this challenge.

Hacker 90411 got a score of 100 for challenge 66730 with a difficulty level of 6, so 90411 earned a full score for this challenge.

Only hacker 90411 managed to earn a full score for more than one challenge, so we print the their hacker_id and name as  space-separated values.

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/full-score/problem?isFullScreen=true).

```
SELECT H.hacker_id, 
       H.name 
FROM   submissions S 
       JOIN challenges C 
         ON S.challenge_id = C.challenge_id 
       JOIN difficulty D 
         ON C.difficulty_level = D.difficulty_level 
       JOIN hackers H 
         ON S.hacker_id = H.hacker_id 
            AND S.score = D.score 
GROUP  BY H.hacker_id, 
          H.name 
HAVING Count(S.hacker_id) > 1 
ORDER  BY Count(S.hacker_id) DESC, 
          S.hacker_id ASC; 
```


6.  Ollivander's Inventory
   
  Harry Potter and his friends are at Ollivander's with Ron, finally replacing Charlie's old broken wand.

Hermione decides the best way to choose is by determining the minimum number of gold galleons needed to buy each non-evil wand of high power and age. Write a query to print the id, age, coins_needed, and power of the wands that Ron's interested in, sorted in order of descending power. If more than one wand has same power, sort the result in order of descending age.

Input Format

The following tables contain data on the wands in Ollivander's inventory:

- Wands: The id is the id of the wand, code is the code of the wand, coins_needed is the total number of gold galleons needed to buy the wand, and power denotes the quality of the wand (the higher the power, the better the wand is).

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19502/1458538092-b2a8163a74-ScreenShot2016-03-08at12.13.39AM.png "This is a sample image.")

- Wands_Property: The code is the code of the wand, age is the age of the wand, and is_evil denotes whether the wand is good for the dark arts. If the value of is_evil is 0, it means that the wand is not evil. The mapping between code and age is one-one, meaning that if there are two pairs, (code1, age1) and (code2, age2), then code1!=code2 and . 
  
![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19502/1458538221-18c4092b7d-ScreenShot2016-03-08at12.13.53AM.png "This is a sample image.")

Sample Input

- Wands Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19502/1458538559-51bf29644e-ScreenShot2016-03-21at10.34.41AM.png "This is a sample image.")

- Wands_Property Table: 
  
![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19502/1458538583-fd514566f9-ScreenShot2016-03-21at10.34.28AM.png "This is a sample image.")

Sample Output

9 45 1647 10
12 17 9897 10
1 20 3688 8
15 40 6018 7
19 20 7651 6
11 40 7587 5
10 20 504 5
18 40 3312 3
20 17 5689 3
5 45 6020 2
14 40 5408 1

Explanation

The data for wands of age 45 (code 1):

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19502/1458539700-2f319702ab-ScreenShot2016-03-21at11.23.06AM.png "This is a sample image.")

- The minimum number of galleons needed for 
   wand(age=45, power=2) = 6020
- The minimum number of galleons needed for 
   wand(age=45, power=10) = 1647
The data for wands of age 40 (code 2):

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19502/1458539909-ab79f7ff95-ScreenShot2016-03-21at11.23.14AM.png "This is a sample image.")


- The minimum number of galleons needed for 
   wand(age=40, power=1) = 5408
- The minimum number of galleons needed for 
   wand(age=40, power=3) = 3312
- The minimum number of galleons needed for 
   wand(age=40, power=5) = 7587
- The minimum number of galleons needed for 
   wand(age=40, power=7) = 6018
The data for wands of age 20 (code 4):

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19502/1458540035-d950b9c900-ScreenShot2016-03-21at11.23.25AM.png "This is a sample image.")
- The minimum number of galleons needed for 
   wand(age=20, power=5) = 504
- The minimum number of galleons needed for 
   wand(age=20, power=6) = 7651
- The minimum number of galleons needed for 
   wand(age=20, power=8) = 3688
The data for wands of age 17 (code 5):

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19502/1458540132-79fd7b916b-ScreenShot2016-03-21at11.23.34AM.png "This is a sample image.")

- The minimum number of galleons needed for 
   wand(age=17, power=3) = 5689
- The minimum number of galleons needed for 
   wand(age=17, power=10) = 9897

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/weather-observation-station-1/problem?isFullScreen=true).

```
SELECT a.id, 
       b.age, 
       a.coins_needed, 
       a.power 
FROM   wands a 
       JOIN wands_property b 
         ON a.code = b.code 
WHERE  b.is_evil = 0 
       AND a.coins_needed = (SELECT Min(a1.coins_needed) 
                             FROM   wands a1 
                                    JOIN wands_property b1 
                                      ON a1.code = b1.code 
                             WHERE  b.age = b1.age 
                                    AND a.power = a1.power) 
ORDER  BY a.power DESC, 
          b.age DESC; 
```


7. Chanllenges
   
  Julia asked her students to create some coding challenges. Write a query to print the hacker_id, name, and the total number of challenges created by each student. Sort your results by the total number of challenges in descending order. If more than one student created the same number of challenges, then sort the result by hacker_id. If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.

Input Format

The following tables contain challenge data:

- Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19506/1458521004-cb4c077dd3-ScreenShot2016-03-21at6.06.54AM.png "This is a sample image.")

- Challenges: The challenge_id is the id of the challenge, and hacker_id is the id of the student who created the challenge.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19506/1458521079-549341d9ec-ScreenShot2016-03-21at6.07.03AM.png "This is a sample image.")

Sample Intput 0

- Hackers Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19506/1458521384-34c6866dae-ScreenShot2016-03-21at6.07.15AM.png "This is a sample image.")

- Challenges Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19506/1458521410-befa8e1cd9-ScreenShot2016-03-21at6.07.25AM.png "This is a sample image.")

Sample Output 0

21283 Angela 6
88255 Patrick 5
96196 Lisa 1

Sample Input 1

- Hackers Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19506/1458521469-87036deea3-ScreenShot2016-03-21at6.07.48AM.png "This is a sample image.")

- Challenges Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19506/1458521490-358215cf0b-ScreenShot2016-03-21at6.07.58AM.png "This is a sample image.")

Sample Output 1

12299 Rose 6
34856 Angela 6
79345 Frank 4
80491 Patrick 3
81041 Lisa 1
Explanation

For Sample Case 0, we can get the following details:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19506/1458521677-fd04c384c0-ScreenShot2016-03-21at6.07.38AM.png "This is a sample image.")

Students 5077 and 62743 both created 4 challenges, but the maximum number of challenges created is 6 so these students are excluded from the result.

For Sample Case 1, we can get the following details:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19506/1458521836-24039e7523-ScreenShot2016-03-21at6.08.08AM.png "This is a sample image.")

Students 12299 and 34856 both created 6 challenges. Because 6 is the maximum number of challenges created, these students are included in the result.

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/challenges/problem?isFullScreen=true).

```
Query : -- Use HAVING instead of WHERE since we have to filter on groups
-- Split the total number of counts into 2 pieces
-- First piece will be the largest number 
-- Second piece will be the number which doesn't repeat (Unique) or is available once

select H.hacker_id, H.name, count(C.challenge_id) as total_count
from Hackers H join Challenges C
on H.hacker_id = C.hacker_id
group by H.hacker_id, H.name
having total_count = 
(
select count(temp1.challenge_id) as max_count
    from challenges temp1
    group by temp1.hacker_id
    order by max_count desc
    limit 1
)
or total_count in
(
    select distinct other_counts from (
select H2.hacker_id, H2.name, count(C2.challenge_id) as other_counts
from Hackers H2 join Challenges C2
on H2.hacker_id = C2.hacker_id
group by H2.hacker_id, H2.name
) temp2
    group by other_counts
having count(other_counts) =1);
order by total_count desc, H.hacker_id
```


8. Content Leaderboard
   
  You did such a great job helping Julia with her last coding contest challenge that she wants you to work on this one, too!

The total score of a hacker is the sum of their maximum scores for all of the challenges. Write a query to print the hacker_id, name, and total score of the hackers ordered by the descending score. If more than one hacker achieved the same total score, then sort the result by ascending hacker_id. Exclude all hackers with a total score of  from your result.

Input Format

The following tables contain contest data:

- Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19503/1458522826-a9ddd28469-ScreenShot2016-03-21at6.40.27AM.png "This is a sample image.")

- Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge for which the submission belongs to, and score is the score of the submission. 
  
![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19503/1458523022-771511df90-ScreenShot2016-03-21at6.40.37AM.png "This is a sample image.")

Sample Input

- Hackers Table: 

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19503/1458523374-7ecc39010f-ScreenShot2016-03-21at6.51.56AM.png "This is a sample image.")

- Submissions Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19503/1458523388-0896218137-ScreenShot2016-03-21at6.51.45AM.png "This is a sample image.")

Sample Output

4071 Rose 191
74842 Lisa 174
84072 Bonnie 100
4806 Angela 89
26071 Frank 85
80305 Kimberly 67
49438 Patrick 43
Explanation

Hacker 4071 submitted solutions for challenges 19797 and 49593, so the total score =95 + max(43,96) = 191.

Hacker 74842 submitted solutions for challenges 19797 and 63132, so the total score = max(98,5) + 76 = 174.

Hacker 84072 submitted solutions for challenges 49593 and 63132, so the total score =100 + 0 = 100.

The total scores for hackers 4806, 26071, 80305, and 49438 can be similarly calculated.

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/contest-leaderboard/problem?isFullScreen=true).

```
Query : SELECT h.hacker_id, h.name, SUM(MAX_SCORE.t1) as total_score
FROM Hackers h inner join 
(
    SELECT MAX(s.score) as t1, s.hacker_id  
    FROM Submissions s
    GROUP BY s.challenge_id, s.hacker_id
    HAVING t1 > 0
) AS MAX_SCORE
ON h.hacker_id = MAX_SCORE.hacker_id
GROUP BY h.hacker_id, h.name
ORDER BY total_score DESC, hacker_id ASC;
```


