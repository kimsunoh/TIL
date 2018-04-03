#### REVERSE(varchar)
- varchar를 좌우를 반전시킨다
```sql
SELECT REVERSE('kimsunoh') FROM DUAL
// 출력 : honusmik
```

#### LEFT(varchar, number)
- varchar를 왼쪽에서 부터 number만큼 잘라낸다
```sql
SELECT LEFT('kimsunoh', 4) FROM DUAL
// 출력 : kims
```

#### RIGHT(varchar, number)
- varchar를 오른쪽에서 부터 number만큼 잘라낸다
```sql
SELECT RIGHT('kimsunoh', 5) FROM DUAL
// 출력 : sunoh
```

----
## 참고링크
* [MySQL 5.7 Reference Manual](https://dev.mysql.com/doc/refman/5.7/en/string-functions.html)