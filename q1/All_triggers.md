```

-- Combined Triggers

-- Create single trigger that does both functions
CREATE OR REPLACE TRIGGER trg_university_policy
BEFORE INSERT OR UPDATE OR DELETE ON system_data
FOR EACH ROW
DECLARE
    PRAGMA AUTONOMOUS_TRANSACTION;
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
    
    -- Check if outside business hours
    IF v_day IN (1, 7) OR v_hour < 8 OR v_hour >= 17 THEN
        -- FIRST: Log the violation
        INSERT INTO access_violations (violation_id, user_name, attempted_action, violation_type)
        VALUES (violation_seq.NEXTVAL, USER, v_action,
                CASE WHEN v_day IN (1, 7) THEN 'Sabbath Violation' ELSE 'After Hours' END);
        
        COMMIT;  -- Commit the log entry
        
        -- SECOND: Block the operation
        RAISE_APPLICATION_ERROR(-20001, 'Access denied: Outside business hours');
    END IF;
END;
/
```
