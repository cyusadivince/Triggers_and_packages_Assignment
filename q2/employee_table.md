```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    salary NUMBER,
    department_id NUMBER
);

-- Insert sample data
INSERT INTO employees VALUES (101, 'calvin', 'Doe', 75000, 10);
INSERT INTO employees VALUES (102, 'Klein', 'Smith', 85000, 10);
INSERT INTO employees VALUES (103, 'Kelly', 'Johnson', 65000, 20);
COMMIT;

```
