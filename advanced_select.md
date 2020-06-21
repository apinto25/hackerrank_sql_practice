# Advanced Select

### Type of Triangle
Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

 * Equilateral: It's a triangle with 3 sides of equal length.
 * Isosceles: It's a triangle with 2 sides of equal length.
 * Scalene: It's a triangle with 3 sides of differing lengths.
 * Not A Triangle: The given values of A, B, and C don't form a triangle.

**TRIANGLES table**

<center>

| Column | Type    |
|--------|---------|
| A      | INTEGER |
| B      | INTEGER |
| C      | INTEGER |
</center>
Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.


~~~~sql
SELECT 
    IF(A+B>C AND A+C>B AND B+C>A, IF(
        A=B AND B=C, 'Equilateral', IF(
            A=B OR B=C OR A=C, 'Isosceles', 'Scalene')
        ), 'Not A Triangle')
FROM TRIANGLES;
~~~~

## OCCUPATIONS table

<center>

| Column     | Type   |
|------------|--------|
| Name       | String |
| Occupation | String |
</center>

### The PADS

Generate the following two result sets:

 1. Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: `AnActorName(A)`, `ADoctorName(D)`, `AProfessorName(P)`, and `ASingerName(S)`.
 2. Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:

	There are a total of [occupation_count] [occupation]s.

where `[occupation_count]` is the number of occurrences of an occupation in OCCUPATIONS and `[occupation]` is the lowercase occupation name. If more than one Occupation has the same `[occupation_count]`, they should be ordered alphabetically.

~~~~sql
SELECT CONCAT(NAME, '(', LEFT(OCCUPATION, 1), ')')
FROM OCCUPATIONS
ORDER BY NAME ASC;
SELECT CONCAT('There are a total of ', COUNT(OCCUPATION), ' ', LOWER(OCCUPATION), 's.')
FROM OCCUPATIONS
GROUP BY OCCUPATION
ORDER BY COUNT(OCCUPATION), OCCUPATION;
~~~~

### Occupations

Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output column headers should be Doctor, Professor, Singer, and Actor, respectively.

Note: Print NULL when there are no more names corresponding to an occupation.

















