# Murder_Mystery Project
---

![174092-clue-illustration](https://github.com/Habdoll/Murder_Mystery/assets/145981715/9ccb8387-39e1-4a41-a3b6-d8ab16e6b697)



## Project Overview
---
A crime has taken place and the detective needs our help. The detective has given the crime scene report, but it’s now lost. The information that we have is that it’s a crime scene report and the crime occurred sometime on Jan.15, 2018 and that it took place in SQL City . 


### Tool
---
- SQL online Database.
  - [Download here](https://sqliteonline.com/)
  
### Step 1
---
In order to first have a general view about the crime that has taken place, I wanted to see the "crime_scene_report" table. I filtered the data based on the information I had: the crime type, city, and date.

```sql
SELECT * FROM crime_scene_report 
	WHERE city = 'SQL City' 
    AND date = '20180115' 
    AND type  = 'murder';
```


### Step 2
---
Then I wanted to investigate each of the witnesses, starting with Annabel, searching the "person" table using her first name and address street name, using the SQL query below:

```sql
SELECT * FROM person 
 		WHERE name LIKE 'Annabel%' 
        and address_street_name like 'Franklin Ave'
```


### Step 3
---
The second witness’ information was found by searching the same table for the street name and the last number on that street using the following query:

```sql
SELECT * from person 
		WHERE address_street_name 
        like 'Northwestern Dr' ORDER BY address_number DESC
```


### Step 4
---
Now that we’ve narrowed down information about the 2 witnesses, it is time to explore more about what they know. Looking next at the "interview" table to see information the witnesses shared about the crime, I used this query:
- For the first witness
```sql
SELECT * from interview 
			where person_id = 14887
```
- For the second witness
```sql
SELECT * from interview 
			where person_id = 16371
```


### Step 5
---
Based on these interviews from the witnesses above, I know the suspect was seen on January 9th at the gym and has a membership number that starts with “48Z.” 
we use the following code

```sql
SELECT * from get_fit_now_check_in 
			where check_in_date like 20180109 
            and membership_id like '48Z%'
```


### Step 6
---
I have now narrowed the suspects down to the 2 individuals above. In order to learn the identify of these suspects and considering they are gold members I ran the following query:

```sql

SELECT * from get_fit_now_member 
				WHERE id LIKE '48Z%' and membership_status = 'gold'
```


### Step 7
---
I now know the 2 names of possible suspects. From the witness interviews, I also know the license number the witness saw. The license number is in the "drivers_license" table while the names are in the "person" table, so I need to JOIN these tables in order to have both pieces of information together, to solve who committed the crime. I will do an INNER JOIN so that I only see the rows these tables have in common.

```sql
SELECT * from drivers_license 
			INNER JOIN person on drivers_license.id = person.license_id
            WHERE name = 'Joe Germuska' OR name = 'Jeremy Bowers'
```


 **Therefore, the person who committed the murder was…**
 
       *Jeremy Bowers*
😄
⬛

