출처 : http://www.gurubee.net/lecture/2909

----

```sql
--내 코드
SELECT ID,MAX(KWH) KWH
      ,TRUNC(MAX(V1)+SUM((CASE WHEN E>=KWH THEN KWH-S ELSE E-S END)*V2),-1) COST_SUM
    FROM USE_T T2,CODE_T T1
    WHERE KWH > S
  GROUP BY ID
  ORDER BY ID;

```


```SQL
--정답코드
SELECT u.id
     , u.kwh
     , TRUNC( MAX(v1)
            + SUM((LEAST(u.kwh, c.e) - c.s) * v2)
            , -1) amt
  FROM use_t u
     , code_t c
 WHERE c.s < u.kwh
 GROUP BY u.id, u.kwh
 ORDER BY id
;

```
