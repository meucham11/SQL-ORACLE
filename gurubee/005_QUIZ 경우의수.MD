출처 : http://www.gurubee.net/lecture/2196

# 1번문제 (조합상관X)
### 내코드
```SQL
SELECT CODE
    FROM TEST
UNION ALL
SELECT T1.CODE||'-'||T2.CODE
    FROM TEST T1, TEST T2
  WHERE T1.CODE<T2.CODE
UNION
SELECT R3.CODE1||'-'|| R3.CODE2||'-'|| T1.CODE
    FROM(
        SELECT T1.CODE CODE1, T2.CODE CODE2
            FROM TEST T1, TEST T2
          WHERE T1.CODE<T2.CODE
        ) R3, TEST T1, TEST T2
  WHERE R3.CODE2<T1.CODE;
```

### 답1-1
```SQL
SELECT code
  FROM test
 UNION ALL
SELECT t1.code || '-' || t2.code
  FROM test t1
     , test t2
 WHERE t1.code < t2.code
 UNION ALL
SELECT t1.code || '-' || t2.code || '-' || t3.code
  FROM test t1
     , test t2
     , test t3
WHERE t1.code < t2.code
AND t2.code < t3.code
;
```
### 답1-2
```SQL
SELECT SUBSTR(SYS_CONNECT_BY_PATH(code,'-'),2) code
  FROM test
CONNECT BY PRIOR code < code
  ORDER BY LEVEL, code
;
```

----
# 2번문제 (조합상관O)
```SQL
SELECT SUBSTR(SYS_CONNECT_BY_PATH(CODE,'-'),2) CODE
	FROM T
  CONNECT BY NOCYCLE PRIOR CODE != CODE
  ORDER BY LEVEL,CODE
```
복습완료 21/06/28

