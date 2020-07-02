출처 : http://www.gurubee.net/lecture/2864

----
```
쉽게품
```

```SQL
CREATE TABLE web_log
AS
SELECT '111' id, 'www.gurubee.net' site, '11:10' TM FROM DUAL
UNION ALL SELECT '111', 'www.gurubee.net', '11:11' FROM DUAL
UNION ALL SELECT '111', 'www.imaso.co.kr', '11:12' FROM DUAL
UNION ALL SELECT '111', 'www.imaso.co.kr', '11:13' FROM DUAL
UNION ALL SELECT '111', 'www.gurubee.net', '11:14' FROM DUAL
UNION ALL SELECT '222', 'www.gurubee.net', '11:11' FROM DUAL
UNION ALL SELECT '222', 'www.imaso.co.kr', '11:12' FROM DUAL
UNION ALL SELECT '222', 'www.imaso.co.kr', '11:13' FROM DUAL
UNION ALL SELECT '222', 'www.imaso.co.kr', '11:14' FROM DUAL
;
```

```SQL
SELECT ID,SITE, MIN(TM),COUNT(*)
    FROM(SELECT ID,SITE,TM,SUM(SAME_SITE) OVER(PARTITION BY ID ORDER BY TM) S_GRP
            FROM(SELECT ID,SITE, TM
                ,NVL(LAG(SITE) OVER(PARTITION BY ID ORDER BY TM),SITE) LAG_SITE
                ,DECODE(NVL(LAG(SITE) OVER(PARTITION BY ID ORDER BY TM),SITE), SITE, 0,1) SAME_SITE
                FROM WEB_LOG
                )
        )
  GROUP BY ID,SITE
  ORDER BY ID
```
