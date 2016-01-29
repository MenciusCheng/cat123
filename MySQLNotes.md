
Normally, a database administrator first uses [CREATE USER](http://dev.mysql.com/doc/refman/5.7/en/create-user.html) to create an account and define its nonprivilege characteristics such as its password, whether it uses secure connections, and limits on access to server resources, then uses [GRANT](http://dev.mysql.com/doc/refman/5.7/en/grant.html) to define its privileges. [ALTER USER](http://dev.mysql.com/doc/refman/5.7/en/alter-user.html) may be used to change the nonprivilege characteristics of existing accounts. For example:

```
CREATE USER 'jeffrey'@'localhost' IDENTIFIED BY 'mypass';
GRANT ALL ON db1.* TO 'jeffrey'@'localhost';
GRANT SELECT ON db2.invoice TO 'jeffrey'@'localhost';
ALTER USER 'jeffrey'@'localhost' WITH MAX_QUERIES_PER_HOUR 90;
```

Installing MySQL on Microsoft Windows Using a [noinstall Zip Archive](http://dev.mysql.com/downloads/mysql/)
<http://dev.mysql.com/doc/refman/5.7/en/windows-install-archive.html>
