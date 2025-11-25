```
-- University System Access Policy Implementation

CREATE SEQUENCE violation_seq START WITH 1 INCREMENT BY 1;


CREATE TABLE access_violations (
    violation_id NUMBER PRIMARY KEY,
    user_name VARCHAR2(100),
    attempted_action VARCHAR2(50),
    attempt_time DATE DEFAULT SYSDATE,
    violation_type VARCHAR2(50)
);

-- . Create sample data table
CREATE TABLE system_data (
    id NUMBER PRIMARY KEY,
    data_value VARCHAR2(255),
    created_date DATE DEFAULT SYSDATE
);

CREATE SEQUENCE data_seq START WITH 1 INCREMENT BY 1;

-- 4. Trigger 1: Access Control Enforcement
CREATE OR REPLACE TRIGGER trg_access_control
BEFORE INSERT OR UPDATE OR DELETE ON system_data
FOR EACH ROW
DECLARE
    v_day NUMBER;
    v_hour NUMBER;
    v_action VARCHAR2(10);
BEGIN
    v_day := TO_NUMBER(TO_CHAR(SYSDATE, 'D'));
    v_hour := TO_NUMBER(TO_CHAR(SYSDATE, 'HH24'));
    
    IF INSERTING THEN v_action := 'INSERT';
    ELSIF UPDATING THEN v_action := 'UPDATE';
    ELSE v_action := 'DELETE';
    END IF;
    
    IF v_day IN (1, 7) OR v_hour < 8 OR v_hour >= 17 THEN
        INSERT INTO access_violations (violation_id, user_name, attempted_action, violation_type)
        VALUES (violation_seq.NEXTVAL, USER, v_action,
                CASE WHEN v_day IN (1, 7) THEN 'Sabbath Violation' ELSE 'After Hours' END);
        
        RAISE_APPLICATION_ERROR(-20001, 'Access denied: Outside business hours');
    END IF;
END;
```

-- Test during business hours (Monday-Friday 8AM-5PM)
INSERT INTO system_data (id, data_value) VALUES (data_seq.NEXTVAL, 'Test data');

-- see the violation that had been made
SELECT * FROM access_violations ORDER BY attempt_time DESC;
