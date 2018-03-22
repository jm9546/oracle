# MANUAL UPGRADE
## 11.2.0.4 to 12.1.0.2 
### 소제목
- **runInstaller**
> 회색 박스

```sql


SQL> ALTER SYSTEM SET COMPATIBLE = '12.1.0' SCOPE=SPFILE;
ALTER SYSTEM SET COMPATIBLE = '12.1.0' SCOPE=SPFILE
*
ERROR at line 1:
ORA-32001: write to SPFILE requested but no SPFILE is in use


SQL> ALTER SYSTEM SET COMPATIBLE='12.1.0' SCOPE=SPFILE;

create spfile from pfile;

File created.

SQL> shutdown immediate;
Database closed.
Database dismounted.
ORACLE instance shut down.
SQL> startup 
ORACLE instance started.

Total System Global Area 1224736768 bytes
Fixed Size                  2923824 bytes
Variable Size             436208336 bytes
Database Buffers          771751936 bytes
Redo Buffers               13852672 bytes
Database mounted.
Database opened.

SQL>  ALTER SYSTEM SET COMPATIBLE='12.1.0' SCOPE=SPFILE;

System altered.

```


```
SQL> @/u01/app/oracle/cfgtoollogs/orcl/preupgrade/postupgrade_fixups.sql
Post Upgrade Fixup Script Generated on 2018-03-22 23:47:40  Version: 12.1.0.2 Build: 006
Beginning Post-Upgrade Fixups...

**********************************************************************
Check Tag:     INVALID_OBJECTS_EXIST
Check Summary: Check for invalid objects
Fix Summary:   Invalid objects are displayed and must be reviewed.
**********************************************************************
Fixup Returned Information:
WARNING: --> Database contains INVALID objects prior to upgrade

     The list of invalid SYS/SYSTEM objects was written to
     registry$sys_inv_objs.
     The list of non-SYS/SYSTEM objects was written to
     registry$nonsys_inv_objs unless there were over 5000.
     Use utluiobj.sql after the upgrade to identify any new invalid
     objects due to the upgrade.
**********************************************************************


**********************************************************************
Check Tag:     OLD_TIME_ZONES_EXIST
Check Summary: Check for use of older timezone data file
Fix Summary:   Update the timezone using the DBMS_DST package after upgrade is complete.
**********************************************************************
Fixup Returned Information:
INFORMATION: --> Older Timezone in use

     Database is using a time zone file older than version 18.
     After the upgrade, it is recommended that DBMS_DST package
     be used to upgrade the 12.1.0.2.0 database time zone version
     to the latest version which comes with the new release.
     Please refer to My Oracle Support note number 977512.1 for details.
**********************************************************************


**********************************************************************
Check Tag:     NOT_UPG_BY_STD_UPGRD
Check Summary: Identify existing components that will NOT be upgraded
Fix Summary:   This fixup does not perform any action.
**********************************************************************
Fixup Returned Information:
This fixup does not perform any action.  
If you want to upgrade those other components, you must do so manually.
**********************************************************************


**********************************************************************
                     [Post-Upgrade Recommendations]
**********************************************************************

                        *****************************************
                        ******** Fixed Object Statistics ********
                        *****************************************

Please create stats on fixed objects two weeks
after the upgrade using the command:
   EXECUTE DBMS_STATS.GATHER_FIXED_OBJECTS_STATS;

^^^ MANUAL ACTION SUGGESTED ^^^


           **************************************************
                ************* Fixup Summary ************

 3 fixup routines generated INFORMATIONAL messages that should be reviewed.

*************** Post Upgrade Fixup Script Complete ********************

PL/SQL procedure successfully completed.

SQL> ^C 

SQL> startup
ORA-01081: cannot start already-running ORACLE - shut it down first
SQL>  select * from v$timezone_file;

FILENAME                VERSION     CON_ID
-------------------- ---------- ----------
timezlrg_4.dat                4          0

SQL>  select * from registry$sys_inv_objs;

no rows selected
```

```
SQL> select comp_name, version, status from dba_registry;

COMP_NAME                                                                                                                                                                                                                                                       VERSION                        STATUS
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------ --------------------------------------------
OLAP Catalog                                                                                                                                                                                                                                                    11.2.0.4.0                     OPTION OFF
Spatial                                                                                                                                                                                                                                                         12.1.0.2.0                     UPGRADED
Oracle Multimedia                                                                                                                                                                                                                                               12.1.0.2.0                     VALID
Oracle XML Database                                                                                                                                                                                                                                             12.1.0.2.0                     VALID
Oracle Text                                                                                                                                                                                                                                                     12.1.0.2.0                     VALID
Oracle Workspace Manager                                                                                                                                                                                                                                        12.1.0.2.0                     VALID
Oracle Database Catalog Views                                                                                                                                                                                                                                   12.1.0.2.0                     UPGRADED
Oracle Database Packages and Types                                                                                                                                                                                                                              12.1.0.2.0                     UPGRADED
JServer JAVA Virtual Machine                                                                                                                                                                                                                                    12.1.0.2.0                     VALID
Oracle XDK                                                                                                                                                                                                                                                      12.1.0.2.0                     VALID
Oracle Database Java Packages                                                                                                                                                                                                                                   12.1.0.2.0                     VALID

COMP_NAME                                                                                                                                                                                                                                                       VERSION                        STATUS
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------ --------------------------------------------
OLAP Analytic Workspace                                                                                                                                                                                                                                         12.1.0.2.0                     VALID
Oracle OLAP API                                                                                                                                                                                                                                                 12.1.0.2.0                     VALID

13 rows selected.
```

```
