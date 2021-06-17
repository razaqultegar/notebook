# MySQL

<div style="text-align:center"><img src="https://upload.wikimedia.org/wikipedia/id/a/a9/MySQL.png" alt="Image by Wikipedia"/></div>

[MySQL](https://www.mysql.com) is an open-source relational database management system (RDBMS). A relational database organizes data into one or more data tables in which data types may be related to each other; these relations help structure the data. SQL is a language programmers use to create, modify and extract data from the relational database, as well as control user access to the database.

## Table Of Contents

1. [Disable ONLY_FULL_GROUP_BY](#disable-only_full_group_by)

## Disable ONLY_FULL_GROUP_BY

Remove ONLY_FULL_GROUP_BY from mysql console:

```bash
mysql > SET GLOBAL sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY',''));
```
