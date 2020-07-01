출처 : http://www.gurubee.net/lecture/2863

----
```
오우..
```

```SQL
--내코드
SELECT MIN(DECODE(WD,1,DAY)) 일요일
      ,MIN(DECODE(WD,2,DAY)) 월요일
      ,MIN(DECODE(WD,3,DAY)) 화요일
      ,MIN(DECODE(WD,4,DAY)) 수요일
      ,MIN(DECODE(WD,5,DAY)) 목요일
      ,MIN(DECODE(WD,6,DAY)) 금요일
      ,MIN(DECODE(WD,7,DAY)) 토요일
        FROM(SELECT DT+LEVEL-1 DT
              , TO_CHAR(DT+LEVEL-1,'D') WD 
              , TO_CHAR(DT+LEVEL-1,'DD') DAY
              , TO_CHAR(DT+LEVEL,'IW') WEEKNUM
                    FROM(SELECT TO_DATE('201402','YYYYMM') DT FROM DUAL)
                  CONNECT BY LEVEL <= LAST_DAY(DT)-DT +1
            )
  GROUP BY WEEKNUM
  ORDER BY WEEKNUM
```



```SQL
--정답코드
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
