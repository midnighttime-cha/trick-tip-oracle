
# SQL for Oracle

## Get all column name
```sql
SELECT table_name, column_name, data_type, data_length
FROM USER_TAB_COLUMNS
WHERE table_name = 'MYTABLE'
```

## Table Modify
```sql
ALTER TABLE TEST_PROJECT2 MODIFY proj_name VARCHAR2(300);
```

## Reset password sys
```bash
sqlplus /nolog
connect / as sysdba
```
next
```sql
ALTER USER sys IDENTIFIED BY "new_password";
```
## Get sequence next value
```sql
SELECT "APP_DBA"."TABLE_TEST_SEQ".nextval ID FROM DUAL
```

## Get sequence last value
```sql
SELECT last_number
FROM user_sequences
WHERE sequence_name = 'TABLE_TEST_SEQ';
```

## Reset sequence last value
```sql
ALTER SEQUENCE TABLE_TEST_SEQ RESTART START WITH 10;
```

## Instance

### Selct instance
```sql
select instance_name from v$instance;
select version from v$instance;
```


## Tablespace

### DROP TABLESPACE and TEMPORARY

Delete Tablespace
```sql
DROP TABLESPACE tbs_01 
    INCLUDING CONTENTS 
        CASCADE CONSTRAINTS;
```

Delete tablespace and datafile
```sql
DROP TABLESPACE tbs_02
   INCLUDING CONTENTS AND DATAFILES;
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
CREATE USER EX_DBA IDENTIFIED BY 12345;
```

## ORA-01940: cannot drop a user that is currently connected
```sql
SELECT s.sid, s.serial#, s.status, p.spid FROM v$session s, v$process p WHERE s.username = 'TEST_DBA' AND p.addr(+) = s.paddr;
# Output

```
next
```sql
ALTER SYSTEM KILL SESSION '<SID>, <SERIAL>';
```


## CREATE TABLESPACE
```sh
CREATE TABLESPACE DATA_EX DATAFILE '/home/oracle/oradata/DATAFILE/DATA_EX01.dbf' SIZE 4096M AUTOEXTEND ON NEXT 100M EXTENT MANAGEMENT LOCAL UNIFORM SIZE 1M;
```

## CREATE TEMPORARY
```sh
CREATE TEMPORARY TABLESPACE TEMP_EX TEMPFILE '/home/oracle/oradata/DATAFILE/TEMP_EX01.dbf' SIZE 3G EXTENT MANAGEMENT LOCAL UNIFORM SIZE 1M;
```

## GRANT DBA
```sh
GRANT RESOURCE,CONNECT TO EX_DBA;
```
Optional
```sql
GRANT EXP_FULL_DATABASE TO EX_DBA;
GRANT IMP_FULL_DATABASE TO EX_DBA;
GRANT CREATE ANY DIRECTORY TO EX_DBA;
```

## CREATE/ALTER USER
```bash
CREATE USER EX_DBA IDENTIFIED BY Test12345 DEFAULT TABLESPACE DATA_EX TEMPORARY YABLESPACE TEMP_EX;

#or

ALTER USER TEST_DBA DEFAULT TABLESPACE DATA_EX;
ALTER USER TEST_DBA TEMPORARY TABLESPACE TEMP_EX;
```
## EXPORT DATAPUMP
```sh
expdp system/SystemPass@XE directory=DATA_PUMP_DIR dumpfile=DATA_EXAMPLE.DMP logfile=DATA_EXAMPLE.log schemas=DATA_EXAMPLE
```

## IMPORT DATAPUMP
```sh
impdp system/SystemPass@XE directory=DATA_PUMP_DIR dumpfile=DATA_EXAMPLE.DMP logfile=DATA_EXAMPLE.log schemas=DATA_EXAMPLE
```

## SHOW DIRECTORY
```sh
SELECT * FROM DBA_DIRECTORIES;
```
