# BASIC JOIN

## CITY and COUNTRY tables

<center>Table 1: CITY</center>
<center>

| Title       | Type         |
|-------------|--------------|
| ID          | NUMBER       |
| NAME        | VARCHAR (17) |
| COUNTRYCODE | VARCHAR (3)  |
| DISCTRICT   | VARCHAR (20) |
| POPULATION  | NUMBER       |
</center>
<br>
<center>Table 2: COUNTRY</center>
<center>

| Title          | Type         |
|----------------|--------------|
| CODE           | VARCHAR (3)  |
| NAME           | VARCHAR (44) |
| CONTINENT      | VARCHAR (13) |
| REGION         | VARCHAR (25) |
| SURFACEAREA    | NUMBER       |
| INDEPYEAR      | VARCHAR (5)  |
| POPULATION     | NUMBER       |
| LIFEEXPECTANCY | VARCHAR (4)  |
| GND            | NUMBER       |
| GNPOLD         | VARCHAR (9)  |
| LOCALNAME      | VARCHAR (44) |
| GOVERNMENTFORM | VARCHAR (44) |
| HEADOFSTATE    | VARCHAR (32) |
| CAPITAL        | VARCHAR (4)  |
| CODE2          | VARCHAR (2)  |
</center>

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

### Asian Population
Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.

~~~~sql
SELECT SUM(CITY.POPULATION)
FROM CITY INNER JOIN COUNTRY
ON CITY.COUNTRYCODE = COUNTRY.CODE
WHERE COUNTRY.CONTINENT = 'ASIA';
~~~~

### African Cities
Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.

~~~~sql
SELECT CITY.NAME
FROM CITY INNER JOIN COUNTRY
ON CITY.COUNTRYCODE = COUNTRY.CODE
WHERE COUNTRY.CONTINENT = 'AFRICA';
~~~~

### Average Population of Each Continent
Given the CITY and COUNTRY tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.

~~~~sql
SELECT COUNTRY.CONTINENT, FLOOR(AVG(CITY.POPULATION))
FROM COUNTRY INNER JOIN CITY
ON CITY.COUNTRYCODE = COUNTRY.CODE
GROUP BY COUNTRY.CONTINENT;
~~~~

### The Report
You are given two tables: Students and Grades. Students contains three columns ID, Name and Marks.

<center>

| Column | Type    |
|--------|---------|
| ID     | INTEGER |
| NAME   | STRING  |
| MARKS  | INTEGER |
</center> 

Grades contains the following data:

<center>

| Grade | Min_mark | Max_mark|
|-------|----------|---------|
|  1    |  0       |   9     |
|  2    | 10       |  19     |
|  3    | 20       |  29     |
|  4    | 30       |  39     |
|  5    | 40       |  49     |
|  6    | 50       |  59     |
|  7    | 60       |  69     |
|  8    | 70       |  79     |
|  9    | 80       |  89     |
| 10    | 90       | 100     |
</center> 

Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

Write a query to help Eve.
Note: Print "NULL"  as the name if the grade is less than 8.










