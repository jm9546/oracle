숨긴파일 포함해서 ora_testdb로 압축하기 

tar cvzf ora_testdb.tar.gz *

vi /etc/passwd 에서
#oracle:x:500:500::/home/oracle:/bin/bash
oracle:x:500:500::/u01/app/oracle:/bin/bash

[oracle]
/u01/app/oracle/product/10.2.0/bin/relink all...


[작업 상황]
사이트 담당자가 오라클 엔진이 원하는 경로에 설치되지 않았다고 원하는 경로로 변경해달라고 요청하였다.
SID는 그대로이고 경로만 변경하는 작업이다.
기존의 경로는 /home/oracle에 엔진이 설치되어 있었으나, /data/oracle로 엔진 경로를 변경하려 한다.
작업을 할 동안 서비스는 내려도 상관없으니 해당 조치를 취해주길 원한다.

 

 

[기존 환경]
OS : RHEL4
오라클SID : testdb
오라클버전 : 10gR2 Enterprise (10.2.0.4.0) Single
오라클계정홈디렉토리 : /home/oracle
ORACLE_BASE : /home/oracle
컨트롤파일, 리두로그파일, 데이터파일 경로 : /home/oracle/oradata/testdb/
dump파일들이 쌓이는 경로 : /home/oracle/admin/testdb/adump
                                        /home/oracle/admin/testdb/bdump
                                        /home/oracle/admin/testdb/cdump
                                        /home/oracle/admin/testdb/udump
리스너 이름 : LISTENER

 

 

[신규 환경]
OS : RHEL4
오라클SID : testdb
오라클버전 : 10gR2 Enterprise (10.2.0.4.0) Single
오라클계정홈디렉토리 : /data/oracle
ORACLE_BASE : /data/oracle
컨트롤파일, 리두로그파일, 데이터파일 경로 : /data/oracle/oradata/testdb/
dump파일들이 쌓이는 경로 : /data/oracle/admin/testdb/adump
                                        /data/oracle/admin/testdb/bdump
                                        /data/oracle/admin/testdb/cdump
                                        /data/oracle/admin/testdb/udump
리스너 이름 : LISTENER

 

==============

 

1. 기존의 DB를 내린다.
 SQL> shutdown immediate;

 

2. /home/oracle/ 밑의 모든 파일(숨김파일 포함)들을 tar로 압축한다.
 $ cd /home/oracle/
 $ tar cvzf ora_testdb.tar.gz .

 

3. 묶은 tar파일을 새로운 신규 디렉토리로 옮긴다.
 $ mv ora_testdb.tar.gz /data/oracle/

 

4. 옮긴 파일의 압축을 푼다.
 $ cd /data/oracle/
 $ tar xvzf ora_testdb.tar.gz

 

5. 신규 디렉토리의 .bash_profile을 열어 ORACLE_BASE를 변경한다.
 $ cd /data/oracle/
 $ vi .bash_profile
  ORACLE_BASE=/data/oracle
 $ . ./.bash_profile

 

6. 오라클계정의 홈디렉토리를 바꿔준다.
 # vi /etc/passwd 에서 기존의 /home/oracle을 /data/oracle 로 변경 후 적용되도록 오라클 계정을 나갔다가 재로그인한다.

 

7. 신규 디렉토리의 ORACLE_HOME/bin 밑으로 가서 relink all 명령어를 입력한다.
 $ cd $ORACLE_HOME/bin
 $ relink all

 

8. 신규 디렉토리의 ORACLE_HOME/network/admin 밑으로 가서 리스너파일의 ORACLE_HOME 경로부분을 새 경로로 변경해준 후 리스너를 재시작한다.
 $ cd $ORACLE_HOME/network/admin
 $ vi listener.ora
  (ORACLE_HOME = /data/oracle/product/10g)
 $ lsnrctl stop LISTENER
 $ lsnrctl start LISTENER
   ...
  Listener Parameter File   /data/oracle/product/10g/network/admin/listener.ora  // 리스너 경로가 신규 경로로 변경되었는지 확인
  Listener Log File            /data/oracle/product/10g/network/log/listener.log  // 리스너 로그가 신규 경로로 변경되었는지 확인
   ...
  The command completed successfully

 

9. 신규 디렉토리의 pfile에서 덤프파일이 쌓이는 경로 밑 컨트롤파일 등의 새 경로로 변경해준다.(필요시 아카이브 경로도 변경)
 $ vi $ORACLE_HOME/dbs/inittestdb.ora
   audit_file_dest='/data/oracle/admin/testdb/adump'
   background_dump_dest='/data/oracle/admin/testdb/bdump'
   core_dump_dest='/data/oracle/admin/testdb/cdump'
   user_dump_dest='/data/oracle/admin/testdb/udump'
   control_files='/data/oracle/oradata/testdb/control01.ctl',
                     '/data/oracle/oradata/testdb/control02.ctl',
                     '/data/oracle/oradata/testdb/control03.ctl'

 

10. sqlplus로 DB를 마운트까지 올린다.
 $ sqlplus / as sysdba
 SQL> startup mount

 

11. 컨트롤파일을 조회하여 pfile에 명시한 경로와 동일한지 확인한다.
 SQL> select name from v$controlfile;

 

12. 리두로그파일과 데이터파일을 alter 명령어로 신규 경로로 변경해준다.
 SQL> select member from v$logfile;
 SQL> alter database rename
        file '/home/oracle/oradata/testdb/redo01.log'
        to '/data/oracle/oradata/testdb/redo01.log';
  나머지 리두로그도 동일한 작업 반복
 SQL> select name from v$datafile;
 SQL> alter database rename
        file '/home/oracle/oradata/testdb/system01.dbf'
        to '/data/oracle/oradata/testdb/system01.dbf';
  나머지 데이터파일도 동일한 작업 반복
 SQL> select name from v$tempfile;
 SQL> alter database rename
        file '/home/oracle/oradata/testdb/temp01.dbf'
        to '/data/oracle/oradata/testdb/temp01.dbf';

 

13. 필요시 아카이브 모드도 확인한다.
 SQL> archive log list

 

14. DB를 오픈상태로 올린다.
 SQL> alter database open

 

15. 필요시 로그스위치나 파라미터 조회 등으로 정상적으로 변경되었는지 확인해본다.
 SQL> alter system switch logfile; // 여러 번 날려 제대로 아카이브 되는지 alert로그에서 확인
 SQL> show parameter dump  // dump파일들이 쌓일 경로가 제대로 설정되었는지 확인

 

16. alert로그를 보면서 DB를 오픈시킬 때까지의 에러코드가 찍혔는지 확인해본다.
이상이 없을 시 기존의 오라클 디렉토리는 삭제해도 무방하다.
 $ vi /data/oracle/admin/testdb/bdump/alert_testdb.log
 # cd /home/
 # rm -fr oracle

 

17. /etc/oratab 파일에서 기존의 경로를 신규 경로로 변경해준다.
 $ vi /etc/oratab
  testdb:/data/oracle/product/10g:N

 

18. /usr/local/bin 밑의 dbhome, oraenv, coreenv 파일은 bash_profile의 변수값을 물고 가므로 
bash_profile 변수값이 제대로 설정되어 있다면, 바꿔줄 내용은 없다.

 

※ 바꿔준 이후 netca나 dbca 등을 실행하려 할 때 '그런 파일이나 디렉토리가 없음' 이런 에러가 나오면, vi로 netca나 dbca를 열어서 그 안의 JRE경로 등 이전 경로를 신규 경로의 것으로 잡아준 후 실행하면 된다.

 


사용자 인지 못하면
userdel 하고
다시
useradd 하고
배시파일 다시만들고~


/etc/passwd 

oracle55:x:500:500:oracle55:/home/oracle55:/bin/bash
oracle:x:501:500::/home/oracle:/bin/bash
