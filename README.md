# Ex-No-5-Creating-Triggers-using-PL-SQL
# DATE:
# AIM: To create a Trigger using PL/SQL.
# Steps:
Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
Create a trigger named as log_salary-update.
Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
End the trigger.
Update the salary of an employee in employee table.
Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
Display the employee table, salary_log table.
# Program:
```
CREATE TABLE employed(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);
```
CREATE TABLE sal_log (

  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into employed values(1,'dulquer','IT',1000000);
insert into employed values(2,'amal','SALES',500000);
## CREATE EMPLOYEE TABLE:
```
CREATE TABLE employed(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);
```
## Create salary_log table:
```
CREATE TABLE sal_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
```
# PLSQL Trigger code:
```
-- Create the trigger
CREATE OR REPLACE TRIGGER log_sal_update
BEFORE UPDATE ON employed
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employed values(1,'dulquer','IT',1000000);
insert into employed values(2,'amal','SALES',500000);

-- Update the salary of an employee
UPDATE employed
SET salary = 60000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employed;

-- Display the salary_log table
SELECT * FROM sal_log;
```
# OUTPUT:
![image](https://github.com/imthiyas19/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/120353416/5209ce0b-d04f-4112-b307-9e0f208dc5a4)


## RESULT:
Thus , the output has been successfully verified.
