**How to check for session waits in the database**

SELECT DECODE(request,0,'Holder: ','Waiter: ') ||sid sess, id1, id2, lmode, request, type FROM V$LOCK WHERE (id1, id2, type) IN (SELECT id1, id2, type FROM V$LOCK WHERE request > 0) ORDER BY id1, request;

**How to check the status of the holding session,last execution time** 

select sid,COMMAND,status,last_call_et, sql_id,PREV_SQL_ID, SERIAL# from v$session where sid= 999;

**How to check the sql text from sqlID** 

select SQL_TEXT from v$sql where  SQL_ID='XXXXX';

**How to check total no sessions in the database** 

select count(1) from v$session ;

**How to check how many  dB sessions are used per host** 

select MACHINE,count(1) from v$session group by MACHINE

select status,count(1) from v$session group by status 

**How to check the current running sqls in the database

SELECT s.username,s.sid,s.serial#,a.sql_text,s.logon_time,s.machine,s.sql_id FROM v$sqlarea  a,v$session s WHERE a.address = s.sql_address AND a.users_executing > 0 order by a.sql_text;


**How to check the currnet locked sessions in the database.
