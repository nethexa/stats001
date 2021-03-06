Automatic Stats for this query:

```sql
SELECT calldate, src, dst, disposition, billsec, ceil ((billsec) / 60)
FROM cdr
WHERE calldate LIKE '2013-01-%'
AND src = '2431'
AND dst LIKE '______%'
AND disposition = 'ANSWERED'
OR calldate LIKE '2013-01-%'
AND src LIKE '______%'
AND dst = '2431'
AND disposition = 'ANSWERED';
```

New Query:

```sql
SELECT calldate, src, dst, disposition, billsec, ceil ((billsec) / 60) AS minutes
FROM cdr
WHERE calldate BETWEEN '2013-01-01 00:00:00' AND '2013-01-02 23:59:59'
AND disposition = 'ANSWERED'
AND (src = '2431' OR dst = '2431')
AND (src LIKE '______%' OR dst LIKE '______%')
ORDER BY calldate ASC;
```

Install Instructions:

```sh
# For this you need curl and php installed.
sudo curl -s http://getcomposer.org/installer | php

# For this you need git installed
sudo ./composer.phar install

sudo chown www-data:\ -R web/includes/

mysql -u user -p < scripts/stats001.sql

# Edit web/index.php and add user and password for MySQL
```

Finally go to [http://localhost/stats001/web/](http://localhost/stats001/web/) and use `admin` and `admin`.
