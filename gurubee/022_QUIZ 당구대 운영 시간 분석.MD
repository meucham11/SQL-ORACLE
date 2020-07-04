출처 : http://www.gurubee.net/lecture/2866

----

```
두 열을 한열로 하는 방법 익숙해져 가는것 같다.
```

```SQL
SELECT stm, etm, cnt
     , SUM( TO_DATE(etm, 'hh24:mi')
          - TO_DATE(stm, 'hh24:mi')
          )*24*60 use_time 
  FROM (SELECT stm
             , SUM(cnt) OVER(ORDER BY stm) cnt
             , LEAD(stm, 1, '21:00')
               OVER(ORDER BY stm) etm
          FROM (SELECT '11:00' stm, 0 cnt FROM dual
                 UNION ALL
                SELECT DECODE(s, 1, stm, etm) stm
                     , SUM(s) cnt
                  FROM t
                     , (SELECT 3-LEVEL*2 s FROM dual
                         CONNECT BY LEVEL < = 2)
                 GROUP BY DECODE(s, 1, stm, etm)
                )
        )
 GROUP BY cnt, ROLLUP((stm, etm))
 ORDER BY stm, cnt
;
```
