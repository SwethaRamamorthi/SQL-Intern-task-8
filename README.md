## SQL Intern task-8
TASK-8 : Stored Procedure and Functions
## Objectives
To learn how to write **reusable SQL blocks** using:
- **Stored Procedures** to perform predefined database operations
- **Stored Functions** to return calculated values

This task focuses on **modularizing SQL logic** using parameters and conditional operations.
## Tools Used
- MySQL Workbench
- ## concepts covered
- 
| Concept             | Description                                                              
|---------------------|--------------------------------------------------------------------------
| Stored Procedure     | A precompiled SQL block that performs an action when called (`CALL`)    
| Stored Function      | Returns a value and can be used in queries like a built-in function     
| DELIMITER            | Used to define the start and end of a block when semicolons are       usedinside             |

| Parameters           | Inputs that can be passed to procedures/functions                       
| Conditional Logic    | Logic such as calculations or WHERE conditions used within blocks           
## Sample Table
REATE TABLE employees (
    emp_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10, 2)
);

INSERT INTO employees (name, salary) VALUES
('Arun', 40000),
('Meena', 60000),
('Raj', 75000);

1.Stored Procedure: IncreaseSalary
 Definition:

 DELIMITER //
CREATE PROCEDURE IncreaseSalary (
    IN empId INT,
    IN percent DECIMAL(5,2)
)
BEGIN
    UPDATE employees
    SET salary = salary + (salary * percent / 100)
    WHERE emp_id = empId;
END //
DELIMITER ;

## Usage:
CALL IncreaseSalary(1, 10); -- Increases salary of emp_id 1 by 10%

2.Stored Function: GetYearlySalary
 Definition:
 
 DELIMITER //
CREATE FUNCTION GetYearlySalary (
    monthly DECIMAL(10,2)
)
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    RETURN monthly * 12;
END //
DELIMITER ;

## Usage:
SELECT name, salary, GetYearlySalary(salary) AS yearly_salary
FROM employees;

## Drop if Needed:
DROP PROCEDURE IF EXISTS IncreaseSalary;
DROP FUNCTION IF EXISTS GetYearlySalary;


| Type      | Name              | Purpose                                      |
| --------- | ----------------- | -------------------------------------------- |
| Procedure | `IncreaseSalary`  | Increases employee salary by a given %       |
| Function  | `GetYearlySalary` | Calculates annual salary from monthly salary |

## Outcome:

1.Learned how to write and execute stored procedures and functions
2.Understood the use of parameters and conditional logic inside SQL blocks
3.Learned how to use the DELIMITER command to manage block structures
4.Gained the ability to modularize SQL logic for clean and reusable code

