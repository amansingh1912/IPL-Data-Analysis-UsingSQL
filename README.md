# IPL Data Analysis Using SQL

I did an analysis on the IPL dataset which I got from Kaggle and I came up with a few questions based on the dataset and answered them through SQL queries as shown below:

### [Link To Dataset](https://drive.google.com/file/d/1lzx7eiWxupFCuIDk4B8io0AwB1ql5Uq5/view?usp=share_link)

## Tool Used: MYSQL

Q1) Find which team played the most matches overall.

### Ans:
## Code:

with t1 as
(
SELECT `team1`
from ipl_dataset
UNION ALL
select `team2`
from ipl_dataset
)
SELECT `team1`, count(*) as Total from t1
group by 1
order by 2 desc
limit 1;

## Output:

![image](https://user-images.githubusercontent.com/72240938/224527201-e54f5ca8-7899-4ceb-9f77-7026702430ed.png)


Q2) Find which team played the most number of matches at their home ground.

### Ans:
## Code:

with t1 as
(
SELECT `team1`
from ipl_dataset
where `team1` = place
UNION ALL
select `team2`
from ipl_dataset
where `team2` = place
)

SELECT `team1`, count(*) as Total from t1
group by 1
order by 2 desc
limit 3;

## Output:

![image](https://user-images.githubusercontent.com/72240938/224527240-3ff7ad38-cc70-4195-88ed-2da9993c5b04.png)


Q3) Find the team from the dataset who hosted and won the most number of matches.

### Ans:
## Code:
with t1 as
(
SELECT team1 from
ipl_dataset
where team1=place and team1=winner
union all
SELECT team2 from 
ipl_dataset
where team2=place and team2=winner
)

SELECT team1, count(*) as Total
from t1
group by 1
order by 2 desc
limit 1;

## Output:
![image](https://user-images.githubusercontent.com/72240938/224527319-6264a4c8-fa9c-40be-b5b6-62915049d1cc.png)



Q4) Who got the most number of man of the matches overall.
### Ans:

## Code:
SELECT man_of_the_match, count(*) as Total_Man_Of_The_Matches
from ipl_dataset
group by man_of_the_match
order by Total_Man_Of_The_Matches desc
limit 5;

## Output:
![image](https://user-images.githubusercontent.com/72240938/224527346-59e35bdd-dca6-4b78-b801-52a6f7ddcf0a.png)



Q5) Find the least score defended.
### Ans:
## Code:

with t1 as
(
SELECT team1, team2, team1_score, team2_score, (team1_score-team2_score) as Difference
from ipl_dataset
)
SELECT min(team1_score) as Least_Score_Defended from t1 
where Difference>0;

## Output:

![image](https://user-images.githubusercontent.com/72240938/224527371-804de37c-8f84-408e-b8bf-4f6116985344.png)



Q6) Find the highest run chased in IPL history.
### Ans:

## Code:
with t1 as
(
SELECT team1_score, team2_score, (team2_score-team1_score) as Difference
from ipl_dataset
)
SELECT max(team2_score) as Highest_Run_Chase from t1
where Difference>0;



## Output:
![image](https://user-images.githubusercontent.com/72240938/224527412-fa75bf91-21ce-4e16-9202-64794ae7eeb9.png)


Q7) Find no. of wins by 1st batting team and 2nd batting team respectively.
### Ans:

## Code:
with t1 as
(
SELECT count(*) as First_batting_team_wins_count
from ipl_dataset
where margin like '%r%'
),
t2 as
(
SELECT count(*) as Chasing_Team_wins_count
from ipl_dataset
where margin like '%w%'
)
SELECT * from t1, t2;

## Output:

![image](https://user-images.githubusercontent.com/72240938/224527467-ef731c30-bef0-494c-8dca-790ba28736be.png)




































