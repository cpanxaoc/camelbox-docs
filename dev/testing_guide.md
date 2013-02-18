#summary A Guide to Tests that come with the Camelbox distribution
#labels Phase-ImplementationPhase-QA

[http://code.google.com/p/camelbox CamelBox Home Page]


= Guide to Testing in Camelbox =

== What should be tested ==
  * JSON package list loads and is valid?
  * GTK C Application runs, displays simple window
  * Gtk2-Perl Demos run
    * Gtk2::GladeXML
    * Gtk2::!GnomeCanvas
    * Gtk2::!GooCanvas
  * SQLite test script can run against a testing database; insert, select, update, delete row
    * [http://www.sqlite.org/sqlite.html Getting started in SQLite]
  * MySQL test script can run against a testing database; insert, select, update, delete row
  * PostgreSQL test script can run against a testing database; insert, select, update, delete row
  * ODBC test script can run against a testing database; insert, select, update, delete row
  * XML file can be parsed with expat wrapper module; test data in XML file

== Testing Library/Network Issues ==

=== Network debugging ===
  * Netcat for Windows (version 1.11)
    * [http://pintday.org/downloads/netcat/nc11nt.zip pintday.org]
    * [http://joncraton.org/files/nc111nt.zip joncraton.org]

=== Windows Tools === 
==== Library/File Usage ====
  * Dependency Walker - You can use [http://www.dependencywalker.com/ Dependency Walker] to help figure out what extra libraries need to be a part of the PAR package (taken from this [http://perlmonks.org/index.pl?node_id=215299 Perl Monks article on shipping apps on Win32]).
  * [http://technet.microsoft.com/en-us/sysinternals/default.aspx Windows SysInternals] - main site
    * [http://technet.microsoft.com/en-us/sysinternals/bb896656.aspx ListDLLs] - Microsoft Technet
    * [http://technet.microsoft.com/en-us/sysinternals/bb896653.aspx ProcessExplorer] - examine processes and files that they have open/loaded
  * Description of using [http://yong321.freeshell.org/computer/orawintrace.html strace] to debug Oracle problems on Windows

==== ODBC ====
  * [http://www.sliksoftware.co.nz/products/odbcview/index.htm ODBCView]

==== SQLServer ====
  * [http://www.sqldbatips.com/showarticle.asp?ID=46 SQL2005 Service Manager]

==== Misc ====
  * [http://sourceforge.net/projects/console Console]

== Test Setup ==
There is a [http://camelbox.googlecode.com/svn/trunk/tests/test_db_server.reg Putty profile] that forwards all of the network ports used for the database s below to a server that can be used for testing.

== Tests that start with 00 ==
Tests that exercise basic functionality

== Tests that start with 10 == 
Basic tests for modules 

== Postgres ==
{{{
# become the DB admin user
sudo su - postgres
# create a user
postgres@calavera:~$ createuser <username>
Shall the new role be a superuser? (y/n) n
Shall the new role be allowed to create databases? (y/n) y
Shall the new role be allowed to create more new roles? (y/n) n
CREATE ROLE
postgres@hostname:~$ psql
postgres=# alter role username with encrypted password 'l33tp@$$w0rd';
ALTER ROLE
postgres=# create database camelbox;
CREATE DATABASE
}}}

User `username` should now be able to log in with the password `l33tp@$$w0rd`.
If MD5 password hashing is turned on, the client will automagically hash the
password before sending it to the remote server.

{{{
postgres@calavera:~$ psql -U username -h 127.0.0.1 -p 15432 -d camelbox
}}}

=== PostgreSQL Links ===
User Management
  * http://www.postgresql.org/docs/8.1/interactive/index.html
  * http://www.postgresql.org/docs/8.1/interactive/role-attributes.html
  * http://www.postgresql.org/docs/8.1/interactive/user-manag.html
  * http://www.postgresql.org/docs/8.1/interactive/tutorial-createdb.html
  * http://www.postgresql.org/docs/8.1/interactive/sql-alterrole.html
DDL 
  * http://www.postgresql.org/docs/8.1/interactive/ddl.html
Windows ODBC Driver:
  * MSI: http://www.postgresql.org/ftp/odbc/versions/msi/
  * DLL zipfile: http://www.postgresql.org/ftp/odbc/versions/dll/

== MySQL ==

{{{
[hostname][user ~]$ mysql -u root -p -h 127.0.0.1 -P 13306
mysql> create user 'username'@'hostname' identified by 'l33tp@$$w0rd';
Query OK, 0 rows affected (0.00 sec)
mysql> create database camelbox;
Query OK, 1 row affected (0.00 sec)
mysql> grant all on camelbox.* to 'username'@'localhost' identified by 'l33tp@$$w0rd';
Query OK, 0 rows affected (0.00 sec)
mysql> \q

[hostname][user ~]$ mysql -u username -p -h 127.0.0.1 -P 13306
}}}

=== MySQL Links ===
User Management
  * http://dev.mysql.com/doc/refman/5.0/en/index.html
  * http://dev.mysql.com/doc/refman/5.0/en/adding-users.html
  * http://dev.mysql.com/doc/refman/5.0/en/create-user.html
DDL 
  * http://dev.mysql.com/doc/refman/5.0/en/data-types.html
  * http://dev.mysql.com/doc/refman/5.0/en/storage-requirements.html
  * http://dev.mysql.com/doc/refman/5.0/en/other-vendor-data-types.html
ODBC Driver for Windows:
  * http://dev.mysql.com/downloads/connector/odbc/5.1.html#win32
== SQLite ==

{{{
sqlite database_name.db
}}}

=== SQLite Links ===
  * Usage example: http://www.sqlite.org/sqlite.html
  * DDL: http://www.sqlite.org/lang.html
  * Datatypes: http://www.sqlite.org/datatype3.html
  * ODBC Driver for Windows: http://www.ch-werner.de/sqliteodbc/

== ODBC ==

=== ODBC Links ===
  * [http://www.easysoft.com/developer/interfaces/odbc/linux.html#odbc_apps_perl Easysoft Linux/UNIX ODBC] - Links to using ODBC in Perl
  * [http://www.easysoft.com/developer/languages/perl/dbd_odbc_tutorial_part_1.html Easysoft DBI/DBD::ODBC Tutorial Part 1]
  * [http://www.easysoft.com/developer/languages/perl/dbd_odbc_tutorial_part_2.html Easysoft DBI/DBD::ODBC Tutorial Part 2]
  * [http://www.foo.be/docs/tpj/issues/vol3_1/tpj0301-0008.html Joe Casadonte's article in The Perl Journal on Win32::ODBC]
  * [http://msdn.microsoft.com/en-us/library/bb208866(loband).aspx SQL Data Types in Access]

<wiki:comment>
vi: set filetype=googlecodewiki shiftwidth=2 tabstop=2 paste:
</wiki:comment>
