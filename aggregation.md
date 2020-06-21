# Aggregation

## CITY table

<center>

| Title       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| NAME        | VARCHAR2 (17) |
| COUNTRYCODE | VARCHAR2 (3)  |
| DISCTRICT   | VARCHAR2 (20) |
| POPULATION  | NUMBER        |
</center>

### Revising Aggregations - The Count Function
Query a count of the number of cities in CITY having a Population larger than 100000.

~~~~sql
SELECT COUNT(NAME)
FROM CITY
WHERE POPULATION > 100000;
~~~~

### Revising Aggregations - The Sum Function
Query the total population of all cities in CITY where District is California.

~~~~sql
SELECT SUM(POPULATION)
FROM CITY
WHERE DISTRICT = 'CALIFORNIA';
~~~~

### Revising Aggregations - Averages
Query the average population of all cities in CITY where District is California.

~~~~sql
SELECT AVG(POPULATION)
FROM CITY
WHERE DISTRICT = 'CALIFORNIA';
~~~~

### Average Population
Query the average population for all cities in CITY, rounded down to the nearest integer.

~~~~sql
SELECT FLOOR(AVG(POPULATION))
FROM CITY;
~~~~

### Japan Population
Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.

~~~~sql
SELECT SUM(POPULATION)
FROM CITY
WHERE COUNTRYCODE = 'JPN';
~~~~

### Population Density Difference
Query the difference between the maximum and minimum populations in CITY.

~~~~sql
SELECT MAX(POPULATION)-MIN(POPULATION)
FROM CITY;
~~~~


### The Blunder
Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's 0 key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeroes removed), and the actual average salary.

<center>

| Column      | Type    |
|-------------|---------|
| ID          | INTEGER |
| NAME        | STRNG   |
| SALARY      | INTEGER |
</center>

Write a query calculating the amount of error (i.e.: actual-miscalculated average monthly salaries), and round it up to the next integer.

Note: Salary is measured in dollars per month and its value is less than 100000.

~~~~sql
SELECT CEIL(AVG(Salary) - AVG(REPLACE(Salary, '0', '')))
FROM EMPLOYEES;
~~~~

### Top Earners
We define an employee's total earnings to be their monthly salary*months worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as 2 space-separated integers.

<center>

| Column      | Type    |
|-------------|---------|
| EMPLOYEE_ID | INTEGER |
| NAME        | STRNG   |
| MONTHS      | INTEGER |
| SALARY      | INTEGER |
</center>

where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is the their monthly salary.

~~~~sql
SELECT (MONTHS*SALARY) AS TOTAL, COUNT(*)
FROM EMPLOYEE
GROUP BY TOTAL
ORDER BY TOTAL DESC
LIMIT 1;
~~~~

## STATION table

<center>

| Title  | Type         |
|--------|--------------|
| ID     | NUMBER       |
| CITY   | VARCHAR (21) |
| STATE  | VARCHAR (2)  |
| LAT_N  | NUMBER       |
| LONG_W | NUMBER       |
</center>
where LAT_N is the northern latitude and LONG_W is the western longitude.

### Weather Observation Station 2
Query the following two values from the STATION table:
 1. The sum of all values in LAT_N rounded to a scale of 2 decimal places.
 2. The sum of all values in LONG_W rounded to a scale of 2 decimal places.

~~~~sql
SELECT ROUND(SUM(LAT_N), 2), ROUND(SUM(LONG_W), 2)
FROM STATION;
~~~~

### Weather Observation Station 13
Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than 38.7880 and less than 137.2345. Truncate your answer to 4 decimal places.

~~~~sql
SELECT ROUND(SUM(LAT_N), 4)
FROM STATION
WHERE LAT_N > 38.7880
AND LAT_N < 137.2345;
~~~~

### Weather Observation Station 14
Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than 137.2345. Truncate your answer to 4 decimal places.

~~~~sql
SELECT ROUND(LAT_N, 4)
FROM STATION
WHERE LAT_N < 137.2345
ORDER BY LAT_N DESC
LIMIT 1;
~~~~

### Weather Observation Station 15
Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than 137.2345. Round your answer to 4 decimal places.

~~~~sql
SELECT ROUND(LONG_W, 4)
FROM STATION
WHERE LAT_N < 137.2345
ORDER BY LAT_N DESC
LIMIT 1;
~~~~

### Weather Observation Station 16
Query the smallest Northern Latitude (LAT_N) from STATION that is greater than 38.7880. Round your answer to 4 decimal places.

~~~~sql
SELECT ROUND(LAT_N, 4)
FROM STATION
WHERE LAT_N > 38.7880
ORDER BY LAT_N ASC
LIMIT 1;
~~~~

### Weather Observation Station 17
Query the Western Longitude (LONG_W)where the smallest Northern Latitude (LAT_N) in STATION is greater than 38.7880. Round your answer to 4 decimal places.

~~~~sql
SELECT ROUND(LONG_W, 4)
FROM STATION
WHERE LAT_N > 38.7880
ORDER BY LAT_N ASC
LIMIT 1;
~~~~

### Weather Observation Station 18
Consider P1(a,b) and P2(c,d) to be two points on a 2D plane.
 * a happens to equal the minimum value in Northern Latitude (LAT_N in STATION).
 * b happens to equal the minimum value in Western Longitude (LONG_W in STATION).
 * c happens to equal the maximum value in Northern Latitude (LAT_N in STATION).
 * d happens to equal the maximum value in Western Longitude (LONG_W in STATION).
Query the Manhattan Distance between points P1 and P2 and round it to a scale of  decimal places.

~~~~sql
SELECT ROUND(ABS(MAX(LAT_N) - MIN(LAT_N)) + ABS(MAX(LONG_W) - MIN(LONG_W)), 4)
FROM STATION;
~~~~

### Weather Observation Station 19
Consider P1(a,b) and P2(c,d) to be two points on a 2D plane where (a,b) are the respective minimum and maximum values of Northern Latitude (LAT_N) and (c,d) are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.

Query the Euclidean Distance between points P1 and P2 and format your answer to display 4 decimal digits.

~~~~sql
SELECT ROUND(SQRT(POWER(MAX(LAT_N)  - MIN(LAT_N),  2) + POWER(MAX(LONG_W) - MIN(LONG_W), 2)), 4)
FROM STATION;
~~~~

### Weather Observation Station 20
A median is defined as a number separating the higher half of a data set from the lower half. Query the median of the Northern Latitudes (LAT_N) from STATION and round your answer to 4 decimal places.

~~~~sql
SELECT ROUND(S.LAT_N, 
FROM STATION AS S
WHERE(SELECT COUNT(Lat_N) FROM STATION WHERE Lat_N < S.LAT_N ) = (SELECT COUNT(Lat_N) FROM STATION WHERE Lat_N > S.LAT_N);
~~~~