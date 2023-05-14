### Basic Select
1. SQL Project Planning 

You are given a table, Projects, containing three columns: Task_ID, Start_Date and End_Date. It is guaranteed that the difference between the End_Date and the Start_Date is equal to 1 day for each row in the table.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12894/1443819551-639948acc0-1.png "This is a sample image.")

If the End_Date of the tasks are consecutive, then they are part of the same project. Samantha is interested in finding the total number of different projects completed.

Write a query to output the start and end dates of projects listed by the number of days it took to complete the project in ascending order. If there is more than one project that have the same number of completion days, then order by the start date of the project.

Sample Input     

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12894/1443819440-1c40e943a1-2.png "This is a sample image.")

Sample Output

2015-10-28 2015-10-29
2015-10-30 2015-10-31
2015-10-13 2015-10-15
2015-10-01 2015-10-04

Explanation

The example describes following four projects:

- Project 1: Tasks 1, 2 and 3 are completed on consecutive days, so these are part of the project. Thus start date of - project is 2015-10-01 and end date is 2015-10-04, so it took 3 days to complete the project.
- Project 2: Tasks 4 and 5 are completed on consecutive days, so these are part of the project. Thus, the start date of project is 2015-10-13 and end date is 2015-10-15, so it took 2 days to complete the project.
- Project 3: Only task 6 is part of the project. Thus, the start date of project is 2015-10-28 and end date is 2015-10-29, so it took 1 day to complete the project.
- Project 4: Only task 7 is part of the project. Thus, the start date of project is 2015-10-30 and end date is 2015-10-31, so it took 1 day to complete the project.

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/sql-projects/problem?isFullScreen=true).

```
Query : SELECT s.Proj_Start_Date, min(e.Proj_End_Date) as Real_Proj_End_Date 
FROM
(SELECT Start_Date as Proj_Start_Date FROM Projects WHERE Start_Date NOT IN (SELECT End_Date FROM Projects)) s,
(SELECT End_Date as Proj_End_Date FROM Projects WHERE End_Date NOT IN (SELECT Start_Date FROM Projects)) e
WHERE s.Proj_Start_Date < e.Proj_End_Date
GROUP BY s.Proj_Start_Date
ORDER BY DATEDIFF(min(e.Proj_End_Date), s.Proj_Start_Date) ASC, s.Proj_Start_Date ASC;
```


2. Placements
   
  You are given three tables: Students, Friends and Packages. Students contains two columns: ID and Name. Friends contains two columns: ID and Friend_ID (ID of the ONLY best friend). Packages contains two columns: ID and Salary (offered salary in $ thousands per month).

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12895/1443820186-2a9b4939a8-1.png "This is a sample image.")

Write a query to output the names of those students whose best friends got offered a higher salary than them. Names must be ordered by the salary amount offered to the best friends. It is guaranteed that no two students got same salary offer.

Sample Input

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12895/1443820079-9bd1e231b1-2_1.png "This is a sample image.")

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12895/1443820100-adb691b2f5-2_2.png "This is a sample image.")

Sample Output

Samantha
Julia
Scarlet

Explanation

See the following table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12895/1443819966-c37c146d27-3.png "This is a sample image.")

Now,

- Samantha's best friend got offered a higher salary than her at 11.55
- Julia's best friend got offered a higher salary than her at 12.12
- Scarlet's best friend got offered a higher salary than her at 15.2
- Ashley's best friend did NOT get offered a higher salary than her

The name output, when ordered by the salary offered to their friends, will be:

- Samantha
- Julia
- Scarlet

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/placements/problem?isFullScreen=true).


```
Query : SELECT S.NAME
FROM STUDENTS S,
     FRIENDS F,
     PACKAGES P1,
     PACKAGES P2
WHERE S.ID = F.ID
  AND F.FRIEND_ID = P2.ID
  AND S.ID = P1.ID
  AND P1.SALARY < P2.SALARY
ORDER BY P2.SALARY;
```

3. Symmetric Pairs
   
  You are given a table, Functions, containing two columns: X and Y.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12892/1443818798-51909e977d-1.png "This is a sample image.")

Two pairs (X1, Y1) and (X2, Y2) are said to be symmetric pairs if X1 = Y2 and X2 = Y1.

Write a query to output all such symmetric pairs in ascending order by the value of X. List the rows such that X1 ≤ Y1.

Sample Input

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/12892/1443818693-b384c24e35-2.png "This is a sample image.")

Sample Output

20 20
20 21
22 23

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/symmetric-pairs/problem?isFullScreen=true).

```
Query : SELECT X,
       Y
FROM FUNCTIONS F1
WHERE EXISTS
    (SELECT *
     FROM FUNCTIONS F2
     WHERE F2.Y = F1.X
       AND F2.X = F1.Y
       AND F2.X > F1.X)
  AND (X != Y)
UNION
SELECT X,
       Y
FROM FUNCTIONS F1
WHERE X = Y
  AND (
         (SELECT COUNT(*)
          FROM FUNCTIONS
          WHERE X = F1.X
            AND Y = F1.X) > 1)
ORDER BY X;
```

4. Interviews
   
  Samantha interviews many candidates from different colleges using coding challenges and contests. Write a query to print the contest_id, hacker_id, name, and the sums of total_submissions, total_accepted_submissions, total_views, and total_unique_views for each contest sorted by contest_id. Exclude the contest from the result if all four sums are 0.

Note: A specific contest can be used to screen candidates at more than one college, but each college only holds 1 screening contest.

Input Format

The following tables hold interview data:

- Contests: The contest_id is the id of the contest, hacker_id is the id of the hacker who created the contest, and name is the name of the hacker.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19596/1458517426-e017c3460e-ScreenShot2016-03-21at4.57.47AM.png "This is a sample image.")

- Challenges: The challenge_id is the id of the challenge that belongs to one of the contests whose contest_id Samantha forgot, and college_id is the id of the college where the challenge was given to candidates.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19596/1458517661-a642f750ce-ScreenShot2016-03-21at4.58.04AM.png "This is a sample image.")

- View_Stats: The challenge_id is the id of the challenge, total_views is the number of times the challenge was viewed by candidates, and total_unique_views is the number of times the challenge was viewed by unique candidates. 

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19596/1458517983-b4302286a8-ScreenShot2016-03-21at4.58.15AM.png "This is a sample image.")

- Submission_Stats: The challenge_id is the id of the challenge, total_submissions is the number of submissions for the challenge, and total_accepted_submission is the number of submissions that achieved full scores.

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19596/1458518090-80983c916a-ScreenShot2016-03-21at4.58.27AM.png "This is a sample image.")

Write a query to output the names of those students whose best friends got offered a higher salary than them. Names must be ordered by the salary amount offered to the best friends. It is guaranteed that no two students got same salary offer.

Sample Input

- Contests Table:
  
![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19596/1458519044-d788f8a6ee-ScreenShot2016-03-21at4.58.39AM.png "This is a sample image.")

- Colleges Table: 

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19596/1458519098-912836d6ac-ScreenShot2016-03-21at4.59.22AM.png "This is a sample image.")

- Challenges Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19596/1458519120-c531743caf-ScreenShot2016-03-21at4.59.32AM.png "This is a sample image.")

- View_Stats Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19596/1458519152-107a67866b-ScreenShot2016-03-21at4.59.43AM.png "This is a sample image.")

- Submission_Stats Table:

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19596/1458519173-091aba871a-ScreenShot2016-03-21at4.59.55AM.png "This is a sample image.")

Sample Output

```
66406 17973 Rose 111 39 156 56
66556 79153 Angela 0 0 11 10
94828 80275 Frank 150 38 41 15
```
Explanation

The contest 66406 is used in the college 11219. In this college 11219, challenges 18765 and 47127 are asked, so from the view and submission stats:

- Sum of total submissions = 27 + 56 + 28 =111

- Sum of total accepted submissions = 10 + 18 + 11 =39

- Sum of total views = 43 + 72 + 26 + 15 =156

- Sum of total unique views = 10 + 13 + 19 + 14 =56

Similarly, we can find the sums for contests 66556 and 94828.

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/placements/problem?isFullScreen=true).


```
Query : SELECT CON.CONTEST_ID,
       CON.HACKER_ID,
       CON.NAME,
       SUM(TOTAL_SUBMISSIONS),
       SUM(TOTAL_ACCEPTED_SUBMISSIONS),
       SUM(TOTAL_VIEWS),
       SUM(TOTAL_UNIQUE_VIEWS)
FROM CONTESTS CON
JOIN COLLEGES COL ON CON.CONTEST_ID = COL.CONTEST_ID
JOIN CHALLENGES CHA ON COL.COLLEGE_ID = CHA.COLLEGE_ID
LEFT JOIN
  (SELECT CHALLENGE_ID,
          SUM(TOTAL_VIEWS) AS TOTAL_VIEWS,
          SUM(TOTAL_UNIQUE_VIEWS) AS TOTAL_UNIQUE_VIEWS
   FROM VIEW_STATS
   GROUP BY CHALLENGE_ID) VS ON CHA.CHALLENGE_ID = VS.CHALLENGE_ID
LEFT JOIN
  (SELECT CHALLENGE_ID,
          SUM(TOTAL_SUBMISSIONS) AS TOTAL_SUBMISSIONS,
          SUM(TOTAL_ACCEPTED_SUBMISSIONS) AS TOTAL_ACCEPTED_SUBMISSIONS
   FROM SUBMISSION_STATS
   GROUP BY CHALLENGE_ID) SS ON CHA.CHALLENGE_ID = SS.CHALLENGE_ID
GROUP BY CON.CONTEST_ID,
         CON.HACKER_ID,
         CON.NAME
HAVING SUM(TOTAL_SUBMISSIONS) != 0
OR SUM(TOTAL_ACCEPTED_SUBMISSIONS) != 0
OR SUM(TOTAL_VIEWS) != 0
OR SUM(TOTAL_UNIQUE_VIEWS) != 0
ORDER BY CONTEST_ID;
```

5. 15 Days of learning SQL
   
  Julia conducted a 15 days of learning SQL contest. The start date of the contest was March 01, 2016 and the end date was March 15, 2016.

Write a query to print total number of unique hackers who made at least 1 submission each day (starting on the first day of the contest), and find the hacker_id and name of the hacker who made maximum number of submissions each day. If more than one such hacker has a maximum number of submissions, print the lowest hacker_id. The query should print this information for each day of the contest, sorted by the date.

Input Format

The following tables hold contest data:

Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker.

![This is a Table image.](Input Format

The following tables hold contest data:

- Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker. "This is a sample image.")

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19597/1458511164-12adec3b8b-ScreenShot2016-03-21at3.26.47AM.png "This is a sample image.")

- Submissions: The submission_date is the date of the submission, submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, and score is the score of the submission. 

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19597/1458511251-0b534030b9-ScreenShot2016-03-21at3.26.56AM.png "This is a sample image.")

Sample Input

For the following sample input, assume that the end date of the contest was March 06, 2016.

- Hackers Table: 

![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19597/1458511957-814a2c7bf2-ScreenShot2016-03-21at3.27.06AM.png "This is a sample image.")

- Submissions Table:
  
![This is a Table image.](https://s3.amazonaws.com/hr-challenge-images/19597/1458512015-ff6a708164-ScreenShot2016-03-21at3.27.21AM.png "This is a sample image.")  

Sample Output

2016-03-01 4 20703 Angela
2016-03-02 2 79722 Michael
2016-03-03 2 20703 Angela
2016-03-04 2 20703 Angela
2016-03-05 1 36396 Frank
2016-03-06 1 20703 Angela
Explanation

On March 01, 2016 hackers 20703, 36396, 54373, and 79722 made submissions. There are 4 unique hackers who made at least one submission each day. As each hacker made one submission, 20703 is considered to be the hacker who made maximum number of submissions on this day. The name of the hacker is Angela.

On March 02, 2016 hackers 15758, 20703, and 79722 made submissions. Now 20703 and 79722 were the only ones to submit every day, so there are 2 unique hackers who made at least one submission each day. 79722 made 2 submissions, and name of the hacker is Michael.

On March 03, 2016 hackers 20703, 36396, and 79722 made submissions. Now 20703 and 79722 were the only ones, so there are 2 unique hackers who made at least one submission each day. As each hacker made one submission so 20703 is considered to be the hacker who made maximum number of submissions on this day. The name of the hacker is Angela.

On March 04, 2016 hackers 20703, 36396, 38289, and 62529 made submissions. Now 20703 and 79722 only submitted each day, so there are 2 unique hackers who made at least one submission each day. As each hacker made one submission so 20703 is considered to be the hacker who made maximum number of submissions on this day. The name of the hacker is Angela.

On March 05, 2016 hackers 20703, 36396, 38289 and 62529 made submissions. Now 20703 only submitted each day, so there is only 1 unique hacker who made at least one submission each day. 36396 made 2 submissions and name of the hacker is Frank.

On March 06, 2016 only 20703 made submission, so there is only 1 unique hacker who made at least one submission each day. 20703 made 1 submission and name of the hacker is Angela.

Link of question [Markdown Live Preview](https://www.hackerrank.com/challenges/15-days-of-learning-sql/problem?isFullScreen=true).


```
Query : /*
SELECT IN SELECT EXPECTS NOT MORE THAN ONE COLUMN
*/
select t.submission_date, t.num, t.id, h.name from
(
    select s.submission_date, 
    (
        select count(distinct(s1.hacker_id)) 
        from Submissions s1 
        where 
        s1.submission_date = s.submission_date and 
        (
            select count(distinct(s2.submission_date)) 
            from Submissions s2 
            where s2.submission_date < s.submission_date and s2.hacker_id = s1.hacker_id
        ) = datediff(s.submission_date, (select min(s3.submission_date) from Submissions s3) )
    )as num,
    (
        select s4.hacker_id
        from Submissions s4 
        where s4.submission_date = s.submission_date 
        group by s4.hacker_id 
        order by count(*) desc, s4.hacker_id
        limit 1
    ) as id
    from 
    (
        select distinct(s5.submission_date) 
        from Submissions s5
    ) s
) t, Hackers h
where h.hacker_id = t.id
order by t.submission_date;
```

