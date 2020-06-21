# BASIC SELECT
## CITY table

<center>

| Title      | Type         |
|------------|--------------|
| ID         | NUMBER       |
| CITY       | VARCHAR (17) |
| STATE      | VARCHAR (3)  |
| DISCTRICT  | VARCHAR (20) |
| POPULATION | NUMBER       |
</center>

### Revising the Select Query I
Query all columns for all American cities in CITY with populations larger than 100000. The CountryCode for America is USA.

~~~~sql
SELECT * 
FROM CITY
WHERE COUNTRYCODE = 'USA'
AND POPULATION > 100000;
~~~~

### Revising the Select Query II
Query the names of all American cities in CITY with populations larger than 120000. The CountryCode for America is USA.

~~~~sql
SELECT NAME
FROM CITY
WHERE COUNTRYCODE = 'USA'
AND POPULATION > 120000;
~~~~

### Select All
Query all columns (attributes) for every row in the CITY table.

~~~~sql
SELECT *
FROM CITY;
~~~~

### Select By ID
Query all columns for a city in CITY with the ID 1661.

~~~~sql
SELECT *
FROM CITY
WHERE ID = 1661;
~~~~

### Japanese Cities' Attributes
Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.

~~~~sql
SELECT *
FROM CITY
WHERE COUNTRYCODE = 'JPN';
~~~~

### Japanese Cities' Names
Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.

~~~~sql
SELECT NAME
FROM CITY
WHERE COUNTRYCODE = 'JPN';
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

### Weather Observation Station 1
Query a list of CITY and STATE from the STATION table.

~~~~sql
SELECT CITY, STATE
FROM STATION;
~~~~

### Weather Observation Station 3
Query a list of CITY names from STATION with even ID numbers only. You may print the results in any order, but must exclude duplicates from your answer.

~~~~sql
SELECT DISTINCT CITY
FROM STATION
WHERE MOD(ID,2) = 0;
~~~~

### Weather Observation Station 4
Let N be the number of CITY entries in STATION, and let N' be the number of distinct CITY names in STATION; query the value of N-N' from STATION. In other words, find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

~~~~sql
SELECT COUNT(CITY) - COUNT(DISTINCT CITY)
FROM STATION;
~~~~

### Weather Observation Station 5
Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

*Sample input:* Let's say that CITY only has four entries: DEF, ABC, PQRS and WXY
*Sample output:* 

	ABC 3
	PQRS 4

When ordered alphabetically, the CITY names are listed as ABC, DEF, PQRS, and WXY, with the respective lengths 3, 3, 4 and 3. The longest-named city is obviously PQRS, but there are 3 options for shortest-named city; we choose ABC, because it comes first alphabetically.

~~~~sql
SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY), CITY LIMIT 1;
SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY) DESC, CITY LIMIT 1;
~~~~

### Weather Observation Station 6
Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

~~~~sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[AEIOU]';
~~~~

### Weather Observation Station 7
Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.

~~~~sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '[AEIOU]$';
~~~~

### Weather Observation Station 8
Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.

~~~~sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[AEIOU].*[AEIOU]$';
~~~~

### Weather Observation Station 9
Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.

~~~~sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^AEIOU])';
~~~~

### Weather Observation Station 10
Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.

~~~~sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '[^AEIOU]$';
~~~~

### Weather Observation Station 11
Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

~~~~sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^AEIOU]'
OR CITY REGEXP '[^AEIOU]$';
~~~~

### Weather Observation Station 12
Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

~~~~sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^AEIOU].*[^AEIOU]$';
~~~~

## STUDENTS TABLE
<center>

| Column | Type    |
|--------|---------|
| ID     | INTEGER |
| NAME   | STRING  |
| MARKS  | INTEGER |
</center>

### Higher Than 75 Marks
Query the Name of any student in STUDENTS who scored higher than 75 Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

~~~~sql
SELECT NAME
FROM STUDENTS
WHERE MARKS > 75
ORDER BY RIGHT(NAME, 3), ID ASC;
~~~~

## EMPLOYEE TABLE
<center>

| Column      | Type    |
|-------------|---------|
| EMPLOYEE_ID | INTEGER |
| NAME        | STRNG   |
| MONTHS      | INTEGER |
| SALARY      | INTEGER |
</center>
where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is their monthly salary.

### Employee Names
Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.

~~~~sql
SELECT NAME
FROM EMPLOYEE
ORDER BY NAME ASC;
~~~~

### Employee Salaries
Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than $2000 per month who have been employees for less than 10 months. Sort your result by ascending employee_id.

~~~~sql
SELECT NAME
FROM EMPLOYEE
WHERE SALARY > 2000
AND MONTHS < 10
ORDER BY EMPLOYEE_ID ASC;
~~~~