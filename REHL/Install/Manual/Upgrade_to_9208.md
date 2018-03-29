ORACLE DB Manual Upgrade
=========================

ORACLE DB Software(9.2.0.8) 설치
--------------------------------


## 9.2.0.4 remove and 9.2.0.8 DB engine install

```
$ cd /u01
$ rm -rf Disk1
$ rm -rf amd
$ unzip p
  /*  압축 해제 후 해당 폴더로 이동  */

$ cd database
$ ./runInstaller
$ netca
```

## PreUpgrade tool
  9i -> 9i로 패치 하기 때문에 bash_profile 수정 X
```
$ sqlplus " / as sysdba"
// 9.2.0.8 DB engine 실행
SQL*Plus: Release 9.2.0.8.0 - Production On Tue Mar 20 00:46:57 2018

Copyright (c) 1982, 2002, Oracle Corporation. All rights reserved.

Connected to an idle instance.

SQL>startup migrate
ORACLE instance started.

Total System Global Area
Fixed Size
Vasriable Size
Database Buffers
Redo 
```



### Warning 1 : timezone file
> $ cd /u01
>
> $ rm -rf Disk
>
> $ rm -rf amd64_db_9204_Disk3.cpio

```
$lsnrctl start
startup migrate
col comp_name for a30
@?/rdbms/admin/catpatch.sql >> $ORACLE_HOME/rdbms/admin/catpatch.sql 실행
shutdown immediate >> DB를 내렸다가 
startup 한다음 
@?/rdbms/admin/utlrp.sql >> $ORACLE_HOME/rdbms/admin/utlrp.sql 수행
```
