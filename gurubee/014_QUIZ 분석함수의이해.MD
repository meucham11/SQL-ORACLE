출처 : http://www.gurubee.net/lecture/2829

----

```
윈도우 함수를 따로 공부하고 오니 쉽게 풀렸다.
```

```
-- 윈도우 함수를 
SELECT YYYYMM, AMT
    , SUM(AMT) OVER(ORDER BY TO_DATE(YYYYMM,'YYYYMM')
                    RANGE BETWEEN INTERVAL '3' MONTH PRECEDING AND INTERVAL '1' MONTH PRECEDING 
                    ) SUM_PRE3
    , SUM(AMT) OVER(ORDER BY TO_DATE(YYYYMM,'YYYYMM')
                    RANGE BETWEEN INTERVAL '1' MONTH FOLLOWING AND INTERVAL '3' MONTH FOLLOWING
                    ) SUM_FOL3
    FROM T;

```
