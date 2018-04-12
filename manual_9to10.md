# MANUAL UPGRADE
## 11.2.0.4 to 12.1.0.2 
### - **runInstaller**
> OUI    

### - **netca**
> OUI 

### - **dbua**
> 수동   

$ vi .bash_profile 
// 10.1.0.2 -> 9.2.0.4 로 수정
$ . .bash_profile

```
[oracle@oracle55 ~]$ sqlplus / as sysdba 
```

```
SQL> startup
SQL> @/u01/app/oracle/product/10.1.0.2/rdbms/admin/preupgrd.sql
```

```
[oracle@oracle55 ~]$ cat upgrade_info.log 
SQL> @/u01/utlu102i.sql
Oracle Database 10.2 Upgrade Information Utility    04-12-2018 03:51:11         
.                                                                               
**********************************************************************          
Database:                                                                       
**********************************************************************          
--> name:       ORCL                                                            
--> version:    9.2.0.8.0                                                       
--> compatible: 9.2.0.0.0                                                       
.                                                                               
**********************************************************************          
Logfiles: [make adjustments in the current environment]                         
**********************************************************************          
--> The existing log files are adequate. No changes are required.               
.                                                                               
**********************************************************************          
Tablespaces: [make adjustments in the current environment]                      
**********************************************************************          
--> SYSTEM tablespace is adequate for the upgrade.                              
.... minimum required size: 572 MB                                              
.... AUTOEXTEND additional space required: 162 MB                               
--> TEMP tablespace is adequate for the upgrade.                                
.... minimum required size: 58 MB                                               
.... AUTOEXTEND additional space required: 18 MB                                
--> CWMLITE tablespace is adequate for the upgrade.                             
.... minimum required size: 16 MB                                               
--> DRSYS tablespace is adequate for the upgrade.                               
.... minimum required size: 27 MB                                               
.... AUTOEXTEND additional space required: 7 MB                                 
--> EXAMPLE tablespace is adequate for the upgrade.                             
.... minimum required size: 151 MB                                              
.... AUTOEXTEND additional space required: 2 MB                                 
--> ODM tablespace is adequate for the upgrade.                                 
.... minimum required size: 10 MB                                               
--> XDB tablespace is adequate for the upgrade.                                 
.... minimum required size: 48 MB                                               
.... AUTOEXTEND additional space required: 3 MB                                 
.                                                                               
**********************************************************************          
Update Parameters: [Update Oracle Database 10.2 init.ora or spfile]             
**********************************************************************          
WARNING: --> "shared_pool_size" needs to be increased to at least 186669875     
WARNING: --> "streams_pool_size" is not currently defined and needs a value of  
at least 50331648                                                               
WARNING: --> "session_max_open_files" needs to be increased to at least 20      
.                                                                               
**********************************************************************          
Deprecated Parameters: [Update Oracle Database 10.2 init.ora or spfile]         
**********************************************************************          
-- No deprecated parameters found. No changes are required.                     
.                                                                               
**********************************************************************          
Obsolete Parameters: [Update Oracle Database 10.2 init.ora or spfile]           
**********************************************************************          
--> "hash_join_enabled"                                                         
.                                                                               
**********************************************************************          
Components: [The following database components will be upgraded or installed]   
**********************************************************************          
--> Oracle Catalog Views         [upgrade]  VALID                               
--> Oracle Packages and Types    [upgrade]  VALID                               
--> JServer JAVA Virtual Machine [upgrade]  VALID                               
...The 'JServer JAVA Virtual Machine' JAccelerator (NCOMP)                      
...is required to be installed from the 10g Companion CD.                       
--> Oracle XDK for Java          [upgrade]  VALID                               
--> Oracle Java Packages         [upgrade]  VALID                               
--> Oracle Text                  [upgrade]  VALID                               
--> Oracle XML Database          [upgrade]  VALID                               
--> Oracle Workspace Manager     [upgrade]  VALID                               
--> Oracle Data Mining           [upgrade]  VALID                               
--> OLAP Analytic Workspace      [upgrade]  UPGRADED                            
--> OLAP Catalog                 [upgrade]  VALID                               
--> Oracle OLAP API              [upgrade]  UPGRADED                            
--> Oracle interMedia            [upgrade]  VALID                               
...The 'Oracle interMedia Image Accelerator' is                                 
...required to be installed from the 10g Companion CD.                          
--> Spatial                      [upgrade]  VALID                               
--> Oracle Ultra Search          [upgrade]  VALID                               
... To successfully upgrade Ultra Search, install it from                       
... the 10g Companion CD.                                                       
.                                                                               
**********************************************************************          
Miscellaneous Warnings                                                          
**********************************************************************          
WARNING: --> Deprecated CONNECT role granted to some user/roles.                
.... CONNECT role after upgrade has only CREATE SESSION privilege.              
WARNING: --> Database contains stale optimizer statistics.                      
.... Refer to the 10g Upgrade Guide for instructions to update                  
.... statistics prior to upgrading the database.                                
.... Component Schemas with stale statistics:                                   
....   SYS                                                                      
....   XDB                                                                      
....   WMSYS                                                                    
....   ODM                                                                      
....   OLAPSYS                                                                  
....   MDSYS                                                                    
....   WKSYS                                                                    
.                                                                               
**********************************************************************          
SYSAUX Tablespace:                                                              
[Create tablespace in the Oracle Database 10.2 environment]                     
**********************************************************************          
--> New "SYSAUX" tablespace                                                     
.... minimum required size for database upgrade: 500 MB                         
.                                                                               

PL/SQL procedure successfully completed.

```

