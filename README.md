# RDBMS_ASSIGNMENT
Below I have explain the approach and shown the output screenshot to my solution:

## Question 1:
Create a database named employee, then import data_science_team.csv, proj_table.csv and emp_record_table.csv into the employee database from the given resources.

### Solution:-

```
CREATE DATABASE employee; 
USE employee;

* After creating the database I Imported the given csv files through GUI of the
  MYSQL Workbench.
```

## Question 2:
Create an ER diagram for the given employee database:

### Solution:-

![MergedImages (2)](https://user-images.githubusercontent.com/122456892/220898377-f57bdd5c-6fa1-4927-a656-a3433e4c3e3d.png)


## Question 3:
Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, and DEPARTMENT from the employee record table, and make a list of employees and details of their department.

### Solution:-

* __Fetching the required data columns from emp_record_table__
```
SELECT ert.EMP_ID, ert.FIRST_NAME, ert.LAST_NAME, ert.GENDER, ert.DEPT
FROM emp_record_table ert;

```
* __Considering ert as an alias for emp_record_table__

### OUTPUT:
<img width="634" alt="Screenshot 2023-02-23 at 2 23 42 PM" src="https://user-images.githubusercontent.com/122456892/220861022-8c94bef9-8ac1-406b-8e21-848102c66b14.png">

## Question 4:
Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPARTMENT, and EMP_RATING if the EMP_RATING is:
* less than two
* greater than four
* between two and four

### Solution:

* Query to fetch required data columns where employee rating(EMP_RATING) is
   LESS THAN 2
```
SELECT ert.EMP_ID, ert.FIRST_NAME, ert.LAST_NAME, ert.GENDER, ert.DEPT , ert.EMP_RATING
FROM emp_record_table ert
WHERE ert.EMP_RATING < 2;
```

### OUTPUT:
<img width="626" alt="Screenshot 2023-02-23 at 2 32 06 PM" src="https://user-images.githubusercontent.com/122456892/220862776-62d48a7e-c02d-4bf2-b0fd-1d58a5a8ede6.png">

* Query to fetch required data columns where employee rating(EMP_RATING) is
  GREATER THAN 4
 
 ```
SELECT ert.EMP_ID, ert.FIRST_NAME, ert.LAST_NAME, ert.GENDER, ert.DEPT, ert.EMP_RATING
FROM emp_record_table ert
WHERE ert.EMP_RATING > 4;
 ```
 
 ### OUTPUT:
 <img width="626" alt="Screenshot 2023-02-23 at 2 33 01 PM" src="https://user-images.githubusercontent.com/122456892/220862935-aa4708de-b4aa-4a44-a53a-8178fd253651.png">

  
* Query to fetch required data columns where employee rating(EMP_RATING) is
  BETWEEN 2 AND 4
  
```
SELECT ert.EMP_ID, ert.FIRST_NAME, ert.LAST_NAME, ert.GENDER, ert.DEPT , ert.EMP_RATING
FROM emp_record_table ert
WHERE ert.EMP_RATING between 2 and 4;
```

### OUTPUT:
<img width="626" alt="Screenshot 2023-02-23 at 2 34 43 PM" src="https://user-images.githubusercontent.com/122456892/220863293-a9edf275-5cf3-4281-b764-2db74dfe1b4d.png">


## Question 5:
Write a query to concatenate the FIRST_NAME and the LAST_NAME of employees in the Finance department from the employee table and then give the resultant column alias as NAME.

### Solution:

```
SELECT CONCAT(ert.FIRST_NAME,' ',ert.LAST_NAME) as NAME 
FROM emp_record_table ert                                
where ert.dept='FINANCE';
```
__Approach:-__

* __Concatenating__ First_name and last name of employees with alias as __NAME__ from emp_record_table where department is __FINANCE__

### OUTPUT:
<img width="626" alt="Screenshot 2023-02-23 at 2 44 10 PM" src="https://user-images.githubusercontent.com/122456892/220865272-0a8cdaeb-7992-4f87-b518-11ee934f0a2c.png">

## Question 6:
Write a query to list only those employees who have someone reporting to them. Also, show the number of reporters (including the President).

### Solution:

```
SELECT mgr.FIRST_NAME,COUNT(*) as number_of_reporters
FROM emp_record_table emp JOIN emp_record_table mgr
ON emp.MANAGER_ID=mgr.EMP_ID
GROUP BY mgr.FIRST_NAME;
```

__Approach:-__

* Fetching the manager name __(employees whom other employees are reporting to)__ by __self joining__ the __emp_record_table__ with itself as manager is     also an employee with specific EMP_ID
* For first table I have given alias as __emp__ to emp_record_table and considering the same table as second table I have given alias as __mgr__

## OUTPUT:-
<img width="626" alt="Screenshot 2023-02-23 at 2 50 20 PM" src="https://user-images.githubusercontent.com/122456892/220866617-9f66494e-b705-4849-91ae-cbe504172a82.png">

## Question 7:
Write a query to list down all the employees from the healthcare and finance departments using union. Take data from the employee record table.

### Solution:-

* __Union__ returns all the __distinct rows__ between the data fetched by two select statements
```
SELECT EMP_ID,FIRST_NAME,LAST_NAME,DEPT - WHERE DEPT='HEALTHCARE'
UNION
SELECT EMP_ID,FIRST_NAME,LAST_NAME,DEPT
FROM emp_record_table WHERE DEPT='FINANCE';
```

__Approach:-__

* Here __First select__ statements fetch all the records __from the emp_record_table__ where __department is Healthcare__
* Union operator combines two select statements and gives distinct rows as result
* Here __Second select__ statements fetch all the records __from the emp_record_table__ where __department is FINANCE__

### OUTPUT:-

<img width="626" alt="Screenshot 2023-02-23 at 2 57 12 PM" src="https://user-images.githubusercontent.com/122456892/220868121-3cb5a086-697d-4598-bbf4-8f35eec179ca.png">

## Question 8:
Write a query to list down employee details such as EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPARTMENT, and EMP_RATING grouped by dept. Also include the respective employee rating along with the max emp rating for the department.

### Solution:-

```
SELECT ert.EMP_ID, ert.FIRST_NAME, ert.LAST_NAME, ert.ROLE, ert.DEPT , ert.EMP_RATING,
MAX(ert.EMP_RATING) OVER(PARTITION BY ert.DEPT) as MAX_RATING_BY_DEPT
FROM emp_record_table ert;
```

__Approach:-__

* Fetching all the required columns asked from the emp_record_table 
* Using __window function__ to calculate __MAX of emp_rating partition by department__ FROM __emp_record_table__ ert; __(Considering ert as alias for       emp_record_table)__

### OUTPUT:-

<img width="718" alt="Screenshot 2023-02-23 at 3 39 09 PM" src="https://user-images.githubusercontent.com/122456892/220877797-aa9c8f57-0650-4326-aeed-2c10eb2c5431.png">

## Question 9:
Write a query to calculate the minimum and the maximum salary of the employees in each role. Take data from the employee record table.

### Solution:-

```
SELECT DISTINCT ROLE,
MAX(ert.SALARY) OVER(PARTITION BY ert.ROLE) AS max_salary, 
MIN(ert.SALARY) OVER(PARTITION BY ert.ROLE) AS min_salary 
FROM emp_record_table ert;
```

__Approach:-__

* In this question we have been asked to fetch the __minimum__ and __maximum__ salary of the employees based on each role, so I have used __window function to fetch the maximum and minimum using aggregate function max and min partition by ROLE(based on each role)__
* Used __DISTINCT Keyword__ here because __window funtion fetch the results in the form of frame__ ,so __duplicate data is returned__ based on the column fetched, so __to avoid redundant data__ I have used DISTINCT Keyword.

### OUTPUT:-
<img width="455" alt="Screenshot 2023-02-23 at 3 45 22 PM" src="https://user-images.githubusercontent.com/122456892/220878937-52c72f31-4f6d-4851-979e-1b5be2519389.png">

## Question 10:
Write a query to assign ranks to each employee based on their experience. Take data from the employee record table.

### Solution:-

```
SELECT EMP_ID,EXP,
DENSE_RANK() OVER(ORDER BY EXP DESC) AS rnk 
FROM emp_record_table;
```

__Approach:-__

* Here I have used __DENSE_RANK()__ function to __assign ranks__ to the employees __based on their experience__
* __Window function__ will assign ranks using __DENSE_RANK order by experience from emp_record_table in descending order__ so that for __highest exp it will rank 1__ and so on.

### OUTPUT:-

<img width="455" alt="Screenshot 2023-02-23 at 3 50 19 PM" src="https://user-images.githubusercontent.com/122456892/220880291-0cce80d1-174d-4d7a-801a-11e66784566b.png">

## Question 11:
Write a query to create a view that displays employees in various countries whose salary is more than six thousand. Take data from the employee record table.

### Solution:-

```
CREATE OR REPLACE VIEW emp_salary_greater_than_six AS 
SELECT EMP_ID,FIRST_NAME,LAST_NAME,COUNTRY,SALARY FROM emp_record_table
WHERE SALARY > 6000;

select * from emp_salary_greater_than_six;
```

__Approach:-__

* Here I created a simple view called __emp_salary_greater_than_six__ which fetches all the records where __salary is greater than 6000__
* I have used __create__ or __replace__ because if __view already exists__ than __replace with the current content__ but if it __does not exists__ than
  __create a view with this content__.
  
### OUTPUT:-

<img width="455" alt="Screenshot 2023-02-23 at 3 58 01 PM" src="https://user-images.githubusercontent.com/122456892/220881679-ba3e8d88-455f-4718-b20e-33d3d8c214fd.png">

## Question 12:
Write a nested query to find employees with experience of more than ten years. Take data from the employee record table.

### Solution:-

```
SELECT *
FROM emp_record_table
WHERE EXP IN (SELECT EXP FROM emp_record_table WHERE EXP > 10);
```

__Approach:-__

* In this particular question to use concept of nested query I have __first fetched the exp from the emp_record_table__ with the condition that __exp > 10__ which will __return all the exp greater than 10__ in the __WHERE CLAUSE__ of the outer select statement and from outer select statement I am fetching __all the records where exp matches with the result of the inner query__ and hence fetch employees with experience more than 10 years
  
### OUTPUT:-

<img width="1015" alt="Screenshot 2023-02-23 at 4 03 41 PM" src="https://user-images.githubusercontent.com/122456892/220882857-faf3523b-6dec-4dcc-9f38-86edbb6cbc0b.png">

## Question 13:
Write a query to create a stored procedure to retrieve the details of the employees whose experience is more than three years. Take data from the employee record table.

### Solution:-

* __NOTE__: __Procedure__ is one of the __subprogram__ where we can store our query to __reuse later__ as and when required
```
DELIMITER $$
CREATE PROCEDURE employeeDetails() 
BEGIN
SELECT * 
FROM emp_record_table 
WHERE EXP > 3;
END $$ 
DELIMITER ;

CALL employeeDetails(); – To call the procedure
```

__Approach:-__
* Here I have created __Procedure name employeeDetails()__ which when called always __returns the details of employees with experience greater than 3__.

### OUTPUT:-
<img width="1019" alt="Screenshot 2023-02-23 at 4 09 03 PM" src="https://user-images.githubusercontent.com/122456892/220883866-a77a6a33-79b6-440c-8fa5-25393889a2ab.png">

## Question 14:
Write a query using stored functions in the project table to check whether the job profile assigned to each employee in the data science team matches the organization’s set standard.
The standard being:
* For an employee with experience less than or equal to 2 years assign __'JUNIOR DATA SCIENTIST'__,
* For an employee with the experience of 2 to 5 years assign __'ASSOCIATE DATA SCIENTIST'__,
* For an employee with the experience of 5 to 10 years assign __'SENIOR DATA SCIENTIST'__,
* For an employee with the experience of 10 to 12 years assign __'LEAD DATA SCIENTIST'__,
* For an employee with the experience of 12 to 16 years assign __'MANAGER'__.

### Solution:-

```
DELIMITER $$
CREATE FUNCTION checkOrganizationStandard() RETURNS tinyint(1)
DETERMINISTIC
BEGIN
DECLARE finished INTEGER DEFAULT 0;
DECLARE v_exp INTEGER;
DECLARE v_role VARCHAR(50);

DECLARE expcursor
CURSOR FOR SELECT exp,role
           FROM data_science_team;
           
-- Declaring the handler to avoid the exception when cursor reaches the end of the row and their is no more rows to fetch
-- Setting finished to 1 which keeps a track of whether exception is generated
 or not, when it is set to 1we exit the loop and no more fetching is done
DECLARE CONTINUE HANDLER FOR NOT FOUND SET finished = 1;
OPEN expcursor;     -- To open the cursor
checkStandard:LOOP

FETCH expcursor INTO v_exp,v_role;
IF finished = 1 THEN LEAVE checkStandard;
END IF;


CASE v_exp
  WHEN v_exp <= 2 THEN
     IF v_role != 'JUNIOR DATA SCIENTIST' THEN 
        RETURN FALSE;
     END IF;
  WHEN v_exp > 2 and v_exp<=5 THEN
     IF v_role != 'ASSOCIATE DATA SCIENTIST' THEN 
        RETURN FALSE;
     END IF;
  WHEN v_exp > 5 and v_exp<=10 THEN
     IF v_role != 'SENIOR DATA SCIENTIST' THEN 
        RETURN FALSE; '
     END IF;
  WHEN v_exp > 10 and v_exp<=12 THEN
     IF v_role != 'LEAD DATA SCIENTIST' THEN 
        RETURN FALSE;
     END IF; 
  ELSE
     IF v_exp > 12 and v_exp<=16 AND v_role != 'MANAGER' THEN 
        RETURN FALSE
     END IF; 
END CASE;
END LOOP checkStandard; 
CLOSE expcursor;
RETURN TRUE; 
END $$ 
DELIMITER ;

 –- Created the procedure which will call the function created above and print
    the message 'Data matches the organization’s set standard' if function
    returns true otherwise 'Data does not matches the organization’s set
    standard' if it return false;

DELIMITER $$
CREATE PROCEDURE checkStandard(OUT res VARCHAR(20)) 
BEGIN
– Calling the function checkOrganizationStandard()
IF(checkOrganizationStandard()) THEN
   SET res= 'Data matches the organization’s set standard';
ELSE
   SET res='Data does not matches the organization’s set standard';
END IF; 
END $$

CALL checkStandard(@res); – Calling the Procedure 
SELECT @res as Result;
```

__Approach:-__

* Created the function __checkOrganizationStandard()__ which checks whether the job profile assigned to each employee in the data science team matches the
  __organization’s set standard__.
    * First Created the function with name checkOrganizationStandard with __Return type tinyint(1)__ as function return boolean value(True(1) or False(0))
    * Function is __Deterministic__ because it always gives the constant output for fixed set of inputs
    * Declare __finished variable__ which will be used later while handling exception to set it to 1 to exit the loop
    * Declaring __v_exp__ variable to fetch exp column data from __data_science_team__ while creating cursor
    * Declaring __v_role__ variable to fetch role column data from __data_science_team__ while creating cursor
    * Creating the __cursor with name expcursor__ which __fetches exp and role__ from __data_science_team__
    * Declaring the __handler__ to __avoid the exception__ when cursor reaches the __end of the row__ and their is no row to fetch
    * Setting finished to 1 which keeps a track of whether __exception is generated or not__, when it is set to 1 we __exit__ the loop and no more
      fetching is done
    * Created Loop that will __fetch each row__ with the help of cursor and then __check the desired condition specified__ and accordingly gives the
      result
    * Fetching the data from the cursor into v_exp and v_role variable
    * In If Condition I checks for if no more rows are left,then exception is generated and finished is set to 1
    * whenever __finished=1__ condition satisfies we __break the loop__ as their is no more rows to traverse
    * Used __Case__ to check for __organization’s set standard__ as per the given question
	           * I have used the CASE over normal If because:- 
	                * ```A simple CASE statement is more readable and efficient than an IF statement when you compare a single expression against a range of 
	                     unique values.
                    ```
                       
             * if __v_exp is less than 2__ then it will hit this when statement where it will check for the __v_role if its 'JUNIOR DATA SCIENTIST'__,if   not it returns false because for the given __v_exp<=2__ role must be __'JUNIOR DATA SCIENTIST'__.
             * if __(2< v_exp <=5)__ then it will hit this when statement where it will check for the __v_role if its 'ASSOCIATE DATA SCIENTIST'__,  if   not it returns false because for the given __(2< v_exp <=5)__ role must be __'ASSOCIATE DATA SCIENTIST'__.
             * if __(5< v_exp <=10)__ then it will hit this when statement where it will check for the __v_role__ if its __'SENIOR DATA SCIENTIST'__,  if not it returns false because for the given __(5< v_exp <=10)__ role must be __'SENIOR DATA SCIENTIST'__.
             * if __(10< v_exp <=12)__ then it will hit this when statement where it will check for the __v_role__ if its __'LEAD DATA SCIENTIST'__,  if   not it returns false because for the given __(10 v_exp <=12)__ role must be __'LEAD DATA SCIENTIST'__.
             * else it will come in this block if none of above satisfies here it check if __(12<v_exp<=16)__ and __v_role__ is not manager then it return false because for the given range role must be __'MANAGER'__.
                       
    * Return True because if all the above condition in loop are not met none of the case returns false that means data is in accordance with
      organization’s set standard 
      
### OUTPUT:-
<img width="570" alt="Screenshot 2023-02-23 at 4 54 27 PM" src="https://user-images.githubusercontent.com/122456892/220892996-8a2cf654-8c64-4ed3-b304-e776d816dd06.png">

      
## Question 15:
Create an index to improve the cost and performance of the query to find the employee whose FIRST_NAME is ‘Eric’ in the employee table after checking the execution plan.


### Solution:-

```
CREATE
INDEX index_first_name
ON emp_record_table(FIRST_NAME);

SELECT *
FROM emp_record_table WHERE FIRST_NAME='Eric';
```

__Approach:-__
* Here I am creating the __index__ on __FIRSTNAME__ attribute of __emp_record_table__ and then after i am fetching the record where __first_name__ is       'Eric'
* __Performance Analysis__
   ```
   * BEFORE CREATING INDEX THE QUERY TOOK 0.00061 sec
   * AFTER CREATING THE INDEX THE QUERY TOOK 0.00052 sec
   ```
* The __difference is not much as we have table with only 19 rows__, so it __doesnt really have much impact__;

### OUTPUT:-
<img width="995" alt="Screenshot 2023-02-23 at 4 56 25 PM" src="https://user-images.githubusercontent.com/122456892/220893235-4b14cb30-6ed7-4953-aca1-f4e77f9418bd.png">

## Question 16:
Write a query to calculate the bonus for all the employees, based on their ratings and salaries (Use the formula: 5% of salary * employee rating).

### Solution:-

```
SELECT EMP_ID,EMP_RATING,SALARY,((0.05 * SALARY)*EMP_RATING) AS BONUS
FROM emp_record_table;
```

__Approach:-__
* Here getting the desired result by performing just the __airthmetic operation__ in select statement

### OUTPUT:-

<img width="494" alt="Screenshot 2023-02-23 at 5 04 05 PM" src="https://user-images.githubusercontent.com/122456892/220894725-4ff09d9f-4ec1-4b4e-a969-0e41badb21a4.png">

## Question 17:
Write a query to calculate the average salary distribution based on the continent and country. Take data from the employee record table.

### Solution:-

```
SELECT DISTINCT CONTINENT,
AVG(SALARY) OVER(PARTITION BY CONTINENT) AS avg_salary_by_continent,
COUNTRY,
AVG(SALARY) OVER(PARTITION BY COUNTRY) AS avg_salary_by_country FROM emp_record_table;
```

__Approach:-__
* Here I have used the __window function__ to get the __average salary by continent__ as well as __average salary by country__.

### OUTPUT:-

<img width="469" alt="Screenshot 2023-02-23 at 5 08 58 PM" src="https://user-images.githubusercontent.com/122456892/220895683-6c65d8f3-b356-4e6b-9aa7-b7dbbb353632.png">






                       










