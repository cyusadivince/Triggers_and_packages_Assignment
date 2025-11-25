```

INSERT INTO access_violations (violation_id, user_name, attempted_action, attempt_time, violation_type)
VALUES (violation_seq.NEXTVAL, 'cyusa', 'INSERT', TO_DATE('2025-01-13 19:30:00', 'YYYY-MM-DD HH24:MI:SS'), 'After Hours');

INSERT INTO access_violations (violation_id, user_name, attempted_action, attempt_time, violation_type)
VALUES (violation_seq.NEXTVAL, 'kevin', 'UPDATE', TO_DATE('2025-01-14 20:15:00', 'YYYY-MM-DD HH24:MI:SS'), 'Sabbath Violation');

INSERT INTO access_violations (violation_id, user_name, attempted_action, attempt_time, violation_type)
VALUES (violation_seq.NEXTVAL, 'anysia', 'DELETE', TO_DATE('2025-01-15 03:45:00', 'YYYY-MM-DD HH24:MI:SS'), 'After Hours');

INSERT INTO access_violations (violation_id, user_name, attempted_action, attempt_time, violation_type)
VALUES (violation_seq.NEXTVAL, 'kalisa', 'INSERT', TO_DATE('2025-11-29 02:00:00', 'YYYY-MM-DD HH24:MI:SS'), 'Sabbath Violation');

-- View the sample violations
SELECT 
    violation_id,
    user_name,
    attempted_action,
    TO_CHAR(attempt_time, 'DD-MON-YYYY HH24:MI:SS') as formatted_time,
    TO_CHAR(attempt_time, 'Day') as day_name,
    violation_type
FROM access_violations 
ORDER BY attempt_time DESC;

-- Summary of violations by type
SELECT 
    violation_type,
    COUNT(*) as violation_count
FROM access_violations 
GROUP BY violation_type;

-- Summary of violations by user
SELECT 
    user_name,
    COUNT(*) as violation_count,
    MAX(attempt_time) as last_violation
FROM access_violations 
GROUP BY user_name
ORDER BY violation_count DESC;

```
