출처 : http://www.gurubee.net/lecture/2909

----

```sql
SELECT ID,MAX(KWH) KWH
      ,MAX(V1)+SUM((CASE WHEN E>=KWH THEN KWH-S ELSE E-S END)*V2) COST_SUM
    FROM USE_T T2,CODE_T T1
    WHERE KWH > S
  GROUP BY ID
  ORDER BY ID;
```
