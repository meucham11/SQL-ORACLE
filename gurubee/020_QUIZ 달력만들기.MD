출처 : http://www.gurubee.net/lecture/2863

----
```
오우..
```


```SQL
SELECT 일, 월, 화, 수, 목, 금, 토
  FROM (SELECT TRUNC  (dt + LEVEL - 1, 'd') w
             , TO_CHAR(dt + LEVEL - 1, 'd') d
             , TO_CHAR(dt + LEVEL - 1, 'dd') dd
        FROM (SELECT TO_DATE('201402','yyyymm') dt FROM dual)
        CONNECT BY LEVEL < = LAST_DAY(dt) - dt + 1
        )
 PIVOT ( MIN(dd) FOR d IN
         (1 일, 2 월, 3 화, 4 수, 5 목, 6 금, 7 토) )
 ORDER BY w
;

```
