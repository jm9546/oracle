# MANUAL UPGRADE
## 11.2.0.4 to 12.1.0.2 
### - **runInstaller**
> OUI    

### - **netca**
> OUI 

### - **dbua**
> 수동   

$ vi .bash_profile 
// 12.1.0.2 -> 11.2.0.4 로 수정
$ . .bash_profile

```
[oracle@oracle55 ~]$ sqlplus / as sysdba 
```

```
SQL> startup
SQL> @/u01/app/oracle/product/12.1.0.2/rdbms/admin/preupgrd.sql
```

```
Loading Pre-Upgrade Package...


***************************************************************************
Executing Pre-Upgrade Checks in ORCL...
***************************************************************************


      ************************************************************

		   ====>> ERRORS FOUND for ORCL <<====

 The following are *** ERROR LEVEL CONDITIONS *** that must be addressed
		    prior to attempting your upgrade.
	    Failure to do so will result in a failed upgrade.


 1) Check Tag:	  COMPATIBLE_PARAMETER
    Check Summary: Verify compatible parameter value is valid
    Fixup Summary:
     ""compatible" parameter must be increased manually prior to upgrade."
    +++ Source Database Manual Action Required +++


 2) Check Tag:	  INVALID_SYS_TABLEDATA
    Check Summary: Check for invalid (not converted) table data
    Fixup Summary:
     "UPGRADE Oracle supplied table data prior to the database upgrade."
    +++ Source Database Manual Action Required +++

	   You MUST resolve the above errors prior to upgrade

      ************************************************************

      ************************************************************

	       ====>> PRE-UPGRADE RESULTS for ORCL <<====

ACTIONS REQUIRED:

1. Review results of the pre-upgrade checks:
 /u01/app/oracle/cfgtoollogs/orcl/preupgrade/preupgrade.log

2. Execute in the SOURCE environment BEFORE upgrade:
 /u01/app/oracle/cfgtoollogs/orcl/preupgrade/preupgrade_fixups.sql

3. Execute in the NEW environment AFTER upgrade:
 /u01/app/oracle/cfgtoollogs/orcl/preupgrade/postupgrade_fixups.sql

      ************************************************************

***************************************************************************
Pre-Upgrade Checks in ORCL Completed.
***************************************************************************

***************************************************************************
***************************************************************************
SQL> EXECUTE DBMS_STATS.GATHER_FIXED_OBJECTS_STATS;


```









```
[oracle@oracle55 ~]$ vi /u01/app/oracle/cfgtoollogs/orcl/preupgrade/preupgrade.log

Oracle Database Pre-Upgrade Information Tool 03-22-2018 22:43:12
Script Version: 12.1.0.2.0 Build: 006
**********************************************************************
   Database Name:  ORCL
  Container Name:  Not Applicable in Pre-12.1 database
    Container ID:  Not Applicable in Pre-12.1 database
         Version:  11.2.0.4.0
      Compatible:  10.2.0.1.0
       Blocksize:  8192
        Platform:  Linux x86 64-bit
   Timezone file:  V4
**********************************************************************
                           [Update parameters]
         [Update Oracle Database 11.2.0.4.0 init.ora or spfile]

--> If Target Oracle is 32-bit, refer here for Update Parameters:
WARNING: --> "processes" needs to be increased to at least 300

--> If Target Oracle is 64-bit, refer here for Update Parameters:
WARNING: --> "processes" needs to be increased to at least 300
**********************************************************************
**********************************************************************
                          [Renamed Parameters]
                     [No Renamed Parameters in use]
**********************************************************************
**********************************************************************
                    [Obsolete/Deprecated Parameters]
             [No Obsolete or Desupported Parameters in use]
**********************************************************************
                            [Component List]
**********************************************************************
--> Oracle Catalog Views                   [upgrade]  VALID
--> Oracle Packages and Types              [upgrade]  VALID
--> JServer JAVA Virtual Machine           [upgrade]  VALID
--> Oracle XDK for Java                    [upgrade]  VALID
--> Oracle Workspace Manager               [upgrade]  VALID
--> OLAP Analytic Workspace                [upgrade]  VALID
--> Oracle Enterprise Manager Repository   [upgrade]  VALID
--> Oracle Text                            [upgrade]  VALID
--> Oracle XML Database                    [upgrade]  VALID
--> Oracle Java Packages                   [upgrade]  VALID
--> Oracle Multimedia                      [upgrade]  VALID
--> Oracle Spatial                         [upgrade]  VALID
--> Data Mining                            [upgrade]  VALID
Oracle Database Pre-Upgrade Information Tool 03-22-2018 22:43:12
Script Version: 12.1.0.2.0 Build: 006
**********************************************************************
   Database Name:  ORCL
  Container Name:  Not Applicable in Pre-12.1 database
    Container ID:  Not Applicable in Pre-12.1 database
         Version:  11.2.0.4.0
      Compatible:  10.2.0.1.0
       Blocksize:  8192
        Platform:  Linux x86 64-bit
   Timezone file:  V4
**********************************************************************
                           [Update parameters]
         [Update Oracle Database 11.2.0.4.0 init.ora or spfile]

--> If Target Oracle is 32-bit, refer here for Update Parameters:
WARNING: --> "processes" needs to be increased to at least 300

--> If Target Oracle is 64-bit, refer here for Update Parameters:
WARNING: --> "processes" needs to be increased to at least 300
**********************************************************************
**********************************************************************
                          [Renamed Parameters]
                     [No Renamed Parameters in use]
**********************************************************************
**********************************************************************
                    [Obsolete/Deprecated Parameters]
             [No Obsolete or Desupported Parameters in use]
**********************************************************************
                            [Component List]
**********************************************************************
--> Oracle Catalog Views                   [upgrade]  VALID
--> Oracle Packages and Types              [upgrade]  VALID
--> JServer JAVA Virtual Machine           [upgrade]  VALID
--> Oracle XDK for Java                    [upgrade]  VALID
--> Oracle Workspace Manager               [upgrade]  VALID
--> OLAP Analytic Workspace                [upgrade]  VALID
--> Oracle Enterprise Manager Repository   [upgrade]  VALID
--> Oracle Text                            [upgrade]  VALID
--> Oracle XML Database                    [upgrade]  VALID
--> Oracle Java Packages                   [upgrade]  VALID
--> Oracle Multimedia                      [upgrade]  VALID
--> Oracle Spatial                         [upgrade]  VALID
--> Data Mining                            [upgrade]  VALID
--> Expression Filter                      [upgrade]  VALID
--> Rule Manager                           [upgrade]  VALID
--> Oracle OLAP API                        [upgrade]  VALID
**********************************************************************
                              [Tablespaces]
**********************************************************************
--> SYSTEM tablespace is adequate for the upgrade.
     minimum required size: 1240 MB
--> UNDOTBS1 tablespace is adequate for the upgrade.
     minimum required size: 400 MB
--> SYSAUX tablespace is adequate for the upgrade.
     minimum required size: 778 MB
--> TEMP tablespace is adequate for the upgrade.
     minimum required size: 60 MB

                      [No adjustments recommended]

**********************************************************************
**********************************************************************
                          [Pre-Upgrade Checks]
**********************************************************************
WARNING: --> Process Count may be too low

     Database has a maximum process count of 150 which is lower than the
     default value of 300 for this release.
     You should update your processes value prior to the upgrade
     to a value of at least 300.
     For example:
        ALTER SYSTEM SET PROCESSES=300 SCOPE=SPFILE
     or update your init.ora file.

ERROR: --> Compatible set too low

     "compatible" currently set at 10.2.0.1.0 and must
     be set to at least 11.0.0 prior to upgrading the database.

     Update your init.ora or spfile to make this change.

WARNING: --> Enterprise Manager Database Control repository found in the database

     In Oracle Database 12c, Database Control is removed during
     the upgrade. To save time during the Upgrade, this action
     can be done prior to upgrading using the following steps after

WARNING: --> Enterprise Manager Database Control repository found in the database

     In Oracle Database 12c, Database Control is removed during
     the upgrade. To save time during the Upgrade, this action
     can be done prior to upgrading using the following steps after
     copying rdbms/admin/emremove.sql from the new Oracle home
   - Stop EM Database Control:
    $> emctl stop dbconsole
                      [No adjustments recommended]

**********************************************************************
**********************************************************************
                          [Pre-Upgrade Checks]
**********************************************************************
WARNING: --> Process Count may be too low

     Database has a maximum process count of 150 which is lower than the
     default value of 300 for this release.
     You should update your processes value prior to the upgrade
     to a value of at least 300.
     For example:
        ALTER SYSTEM SET PROCESSES=300 SCOPE=SPFILE
     or update your init.ora file.

ERROR: --> Compatible set too low

     "compatible" currently set at 10.2.0.1.0 and must
     be set to at least 11.0.0 prior to upgrading the database.

     Update your init.ora or spfile to make this change.

WARNING: --> Enterprise Manager Database Control repository found in the database

     In Oracle Database 12c, Database Control is removed during
     the upgrade. To save time during the Upgrade, this action
     can be done prior to upgrading using the following steps after
     copying rdbms/admin/emremove.sql from the new Oracle home
   - Stop EM Database Control:
    $> emctl stop dbconsole

   - Connect to the Database using the SYS account AS SYSDBA:

   SET ECHO ON;
   SET SERVEROUTPUT ON;
   @emremove.sql
     Without the set echo and serveroutput commands you will not
     be able to follow the progress of the script.

ERROR: --> Invalid Oracle supplied table data found in your database.

     Invalid data can be seen prior to the database upgrade
     or during PDB plug in.  This table data must be made
     valid BEFORE upgrade or plug in.

   - To fix the data, load the Preupgrade package and execute
     the fixup routine.
     For plug in, execute the fix up routine in the PDB.

    @?/rdbms/admin/utluppkg.sql
    SET SERVEROUTPUT ON;
    exec dbms_preup.run_fixup_and_report('INVALID_SYS_TABLEDATA')
    SET SERVEROUTPUT OFF;

WARNING: --> "DMSYS" schema exists in the database

     The DMSYS schema (Oracle Data Mining) will be removed
     from the database during the database upgrade.
     All data in DMSYS will be preserved under the SYS schema.
     Refer to the Oracle Data Mining User's Guide for details.

INFORMATION: --> OLAP Catalog(AMD) exists in database

     Starting with Oracle Database 12c, OLAP Catalog component is desupported.
     If you are not using the OLAP Catalog component and want
     to remove it, then execute the
     ORACLE_HOME/olap/admin/catnoamd.sql script before or
     after the upgrade.

INFORMATION: --> Older Timezone in use

     Database is using a time zone file older than version 18.
     After the upgrade, it is recommended that DBMS_DST package
     be used to upgrade the 11.2.0.4.0 database time zone version
     to the latest version which comes with the new release.
     Please refer to My Oracle Support note number 977512.1 for details.

INFORMATION: --> There are existing Oracle components that will NOT be
     upgraded by the database upgrade script.  Typically, such components
     have their own upgrade scripts, are deprecated, or obsolete.
     Those components are:  OLAP Catalog


**********************************************************************
                      [Pre-Upgrade Recommendations]
**********************************************************************

                        *****************************************
                        ********* Dictionary Statistics *********
                        *****************************************

Please gather dictionary statistics 24 hours prior to
upgrading the database.
To gather dictionary statistics execute the following command
while connected as SYSDBA:
    EXECUTE dbms_stats.gather_dictionary_stats;

^^^ MANUAL ACTION SUGGESTED ^^^


                        *****************************************
                        ************ Existing Events ************
                        *****************************************

Please review and remove any unnecessary events prior to upgrading.
It is strongly recommended that these be removed before upgrade unless
your application vendors and/or Oracle Support state differently.
Changes will need to be made in the init.ora or spfile.



^^^ MANUAL ACTION SUGGESTED ^^^


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

**********************************************************************
                   ************  Summary  ************

 2 ERRORS exist that must be addressed prior to performing your upgrade.
 3 WARNINGS that Oracle suggests are addressed to improve database performance.
 3 INFORMATIONAL messages that should be reviewed prior to your upgrade.

 After your database is upgraded and open in normal mode you must run
 rdbms/admin/catuppst.sql which executes several required tasks and completes
 the upgrade process.

 You should follow that with the execution of rdbms/admin/utlrp.sql, and a
 comparison of invalid objects before and after the upgrade using
 rdbms/admin/utluiobj.sql

 If needed you may want to upgrade your timezone data using the process
 described in My Oracle Support note 1509653.1
                   ***********************************
```

# 1) WARNING1 & ERROR solution


```
[oracle@oracle55 ~]$ cd /u01/app/oracle/product/11.2.0.4/dbs
[oracle@oracle55 ~]$ vi initorcl.ora

//processes=150 => processes=300
//compatible='10.2.0' =>compatible='11.0.0'

```

# 2) WARNING2 solution

```
SQL> SET ECHO ON;
SQL> SET SERVEROUTPUT ON;
SQL> !find /u01 -name emremove.sql
SQL> @emremove.sql
```

# 3) WARNING3 solution
```
SQL> @/u01/app/oracle/product/12.1.0.2/rdbms/admin/utluppkg.sql
SQL> SET SERVEROUTPUT ON;
SQL> exec dbms_preup.run_fixup_and_report('INVALID_SYS_TABLEDATA')
SQL> SET SERVEROUTPUT OFF;
```

# 3) WARNING3 solution
```
SQL> ORACLE_HOME/olap/admin/catnoamd.sql
SQL> EXECUTE dbms_stats.gather_dictionary_stats;
SQL> EXECUTE DBMS_STATS.GATHER_FIXED_OBJECTS_STATS;
SQL> shutdown immediate
SQL> exit
```


# 4) Add solution?
```
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

- ORACLE_HOME
```
$vi .bash_profile
// 11.2.0.4 -> 12.1.0.2 로 수정

$ . .bash_profile
$vi /etc/oratab
// 12.1.0.2 로 수정
```

- CP
```
# cd $ORACLE_HOME/dbs 
# cp $ORACLE_BASE/product/11.2.0.4/dbs/orapworcl . 
# cp $ORACLE_BASE/product/11.2.0.4/dbs/spfileorcl.ora .
```

```
# cd $ORACLE_HOME/network/admin 
# cp $ORACLE_BASE/product/11.2.0.4/network/admin/listener.ora . 
# cp $ORACLE_BASE/product/11.2.0.4/network/admin/sqlnet.ora . 
# cp $ORACLE_BASE/product/11.2.0.4/network/admin/tnsnames.ora .
```

```
# cd $ORACLE_HOME/sqlplus/ 
# cp $ORACLE_BASE/product/11.2.0.4/sqlplus/admin/glogin.sql .
```

```
SQL> startup migrate
> create tablespace sysaux datafile '/u01/app/oracle/oradata/orcl/sysaux01.dbf
> size 600M reuse
> extent management local 
> segment space management auto 
> online;

Tablespace created.
```

- upgrade
```
[oracle@oracle55 ~]$ cd $ORACLE_HOME/rdbms/admin
[oracle@oracle55 admin]$ $ORACLE_HOME/perl/bin/perl catctl.pl -n 4 catupgrd.sql
```


```
SQL> startup
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
