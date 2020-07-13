출처 : http://www.gurubee.net/lecture/2955

----
생각보다 난이도가 쉬웠다.


```sql
SELECT dt
     , COUNT(*) 접속건수
     , COUNT(DISTINCT id) 접속자수
     , SUM(COUNT(*)) OVER(ORDER BY dt) 누적접속건수
     , SUM(COUNT(x)) OVER(ORDER BY dt) 누적접속자수
  FROM (SELECT dt, id
             , DECODE(
               ROW_NUMBER() OVER(
               PARTITION BY id ORDER BY dt)
               , 1, 1) x
          FROM t
        )
 GROUP BY dt
 ORDER BY dt
;

```
