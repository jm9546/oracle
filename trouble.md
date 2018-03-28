###error1

```
dbca
java.io.IOException: Bad file descriptor
  at java.io.FileInptStrem.readBytes
```
[sqlplus.mk] 오류를 방지하기 위해서 이거 하기!

http://rohitguptaoracletips.blogspot.kr/2008/06/common-oracle-installation.html

```
$ mv /usr/bin/gcc /usr/bin/gcc.orig
$ mv /usr/bin/g++ /usr/bin/g++.orig
$ ln -s /usr/bin/x86_64-redhat-linux-gcc32 /usr/bin/gcc
$ ln -s /usr/bin/x86_64-redhat-linux-g++32 /usr/bin/g++

su - oracle
cd $ORACLE_HOME/bin
relink all > relink.txt 2>&1
```

###error2

```
rpm에러
ERROR:Id.so:object '/lib/libcwait.so' from /etc/Id.so.preload cannot be preloaded
```

```
# echo ""> /etc/Id.so.preload
```

###error3
runlnstaller 오류
```
## Checking Network Configuration requirements ... ##
Recommendation: Oracle supports installations on systems with DHCP-assigned public IP addresses.
```
```
///	1.
	vi /etc/hosts
	192.168.137.55 oracle55
----------------------------------------------------------------------------
///	2.vm상에서 RHEL에서 네트워크설정 -> DNS 호스트명 host name을 bash_profile에 호스트네임이랑 일치하게 설정함

	Applications -> System tools -> network Device control -> DNS수정
	host name : 배쉬셀과 일치하게
	praimary : 8.8.8.8
```
  
  ###error4
```
  ORA-01034: ORACLE not available ORA-27101: shared memory realm does not exist Linux-x86_64 Error: 2: No such file or directory
```
http://jangcool.tistory.com/entry/ORA01034-ORACLE-not-available-ORA27101-shared-memory-realm-does-not-exist-Linuxx8664-Error-2-No-such-file-or-directory
```
//1. 
#sqlplus /nolog
#conn sys /as sysdba
#password : 비밀번호 적기
sql>shutdown immediate -- 강제 종료
sql>startup open

//2. 
 listener.ora
 tnsname.ora
```
