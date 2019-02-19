# Java JDBC

## SQL Server 2000
- Jar：msbase.jar、mssqlserver.jar、msutil.jar
- Driver：com.microsoft.jdbc.sqlserver.SQLServerDriver
- URL：jdbc:microsoft:sqlserver://localhost:1433;DatabaseName=XY_CITY;
## SQL Server 2005(JDBC 4.0)
- Jar：sqljdbc.jar(jdk<6)、sqljdbc4.jar(jdk>6)
- driver：com.microsoft.sqlserver.jdbc.SQLServerDriver
- URL：jdbc:sqlserver://localhost:1433;DatabaseName=XY_CITY;
## SQL Server 2008
- Jar：sqljdbc4.jar
- 其他同SQL Server 2005
## SQL Server 2012
- Jar：sqljdbc41.jar(jdk7)、sqljdbc42.jar(jdk8)
- 其他同SQL Server 2005
## JTDS
- jTDS is an open source 100% pure Java（Type 4）JDBC 3.0 driver for Microsoft SQL Server（6.5，7，2000，2005，2008，2012）and Sybase ASE（10，11，12，15）
- https://sourceforge.net/projects/jtds/
- driver：net.sourceforge.jtds.jdbc.Driver
- URL：jdbc:jtds:sqlserver://localhost:1433;DatabaseName=XY_CITY;
- gradle：net.sourceforge.jtds:jtds:1.3.1

## Resource
- https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=11774
- https://docs.microsoft.com/en-us/sql/connect/jdbc/system-requirements-for-the-jdbc-driver?view=sql-server-2017
- https://docs.microsoft.com/zh-cn/sql/connect/jdbc/system-requirements-for-the-jdbc-driver?view=sql-server-2017