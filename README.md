
# SQL for Oracl

## Get all column name
```sql
SELECT table_name, column_name, data_type, data_length
FROM USER_TAB_COLUMNS
WHERE table_name = 'MYTABLE'
```




# รวมการแก้ปัญหา Oracle 12c

## ORA-28014: Cannot Drop Administrative Users
```sql
ALTER SESSION SET "_oracle_script"=true;
DROP USER TEST_DBA CASCADE;
```

## ORA-65096: invalid common user or role name
```sql
ALTER SESSION SET "_oracle_script"=true;
CREATE USER TEST_DBA IDENTIFIED BY 12345;
```

## ORA-01940: cannot drop a user that is currently connected
```sql
SELECT s.sid, s.serial#, s.status, p.spid 
  FROM v$session s, v$process p 
 WHERE s.username = 'TEST' --<<<--
  AND p.addr(+) = s.paddr;
# Output

```
next
```sql
ALTER SYSTEM KILL SESSION '<SID>, <SERIAL>';
```





