출처 : http://www.gurubee.net/lecture/2866

----

```
두 열을 한열로 하는 방법 익숙해져 가는것 같다.
```

```SQL
SELECT POINT STR
      ,NVL(LEAD(POINT) OVER(ORDER BY POINT),'21:00') END 
      ,SUM(TOTAL) OVER(ORDER BY POINT) S_CNT
    FROM(SELECT '11:00' POINT, 0 TOTAL FROM DUAL   
         UNION ALL
        SELECT 
              DECODE(CNT,1,STM,ETM) POINT
              ,SUM(CNT) TOTAL
            FROM T
                ,(SELECT DECODE(LEVEL,2,-1,1) CNT FROM DUAL CONNECT BY LEVEL <=2)
          GROUP BY(DECODE(CNT,1,STM,ETM))
          ORDER BY POINT
          )
```
<img width="109" alt="1" src="https://user-images.githubusercontent.com/34879309/86524086-ff999c00-beb0-11ea-94f1-5114f2b5816a.PNG">
