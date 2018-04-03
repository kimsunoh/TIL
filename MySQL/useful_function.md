#### REVERSE(varchar)
- varchar�� �¿츦 ������Ų��
```sql
SELECT REVERSE('kimsunoh') FROM DUAL
// ��� : honusmik
```

#### LEFT(varchar, number)
- varchar�� ���ʿ��� ���� number��ŭ �߶󳽴�
```sql
SELECT LEFT('kimsunoh', 4) FROM DUAL
// ��� : kims
```

#### RIGHT(varchar, number)
- varchar�� �����ʿ��� ���� number��ŭ �߶󳽴�
```sql
SELECT RIGHT('kimsunoh', 5) FROM DUAL
// ��� : sunoh
```

----
## ����ũ
* [MySQL 5.7 Reference Manual](https://dev.mysql.com/doc/refman/5.7/en/string-functions.html)