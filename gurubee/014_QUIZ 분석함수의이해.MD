출처 : http://www.gurubee.net/lecture/2829

----

```
윈도우 함수를 따로 공부하고 오니 쉽게 풀렸다.
```

```SQL
-- 윈도우 함수를 이용한 풀이
SELECT YYYYMM, AMT
    , SUM(AMT) OVER(ORDER BY TO_DATE(YYYYMM,'YYYYMM')
                    RANGE BETWEEN INTERVAL '3' MONTH PRECEDING AND INTERVAL '1' MONTH PRECEDING 
                    ) SUM_PRE3
    , SUM(AMT) OVER(ORDER BY TO_DATE(YYYYMM,'YYYYMM')
                    RANGE BETWEEN INTERVAL '1' MONTH FOLLOWING AND INTERVAL '3' MONTH FOLLOWING
                    ) SUM_FOL3
    FROM T;
```
또는
```SQL
SELECT YYYYMM, AMT
, SUM(AMT) OVER(ORDER BY TO_DATE(yyyymm,'yyyymm')
				ROWS BETWEEN 3 PRECEDING  
						AND 1 PRECEDING) P1
, SUM(AMT) OVER(ORDER BY TO_DATE(yyyymm,'yyyymm')
				ROWS BETWEEN 1 FOLLOWING
						AND 3 FOLLOWING) P2
FROM T;
-- 결과는 같은데 날짜가 연속형이 아니라면 개월 단위로 뽑는것이 아니기 때문에 첫번째 쿼리가 맞을듯
```
<img width="185" alt="1" src="https://user-images.githubusercontent.com/34879309/85917684-33643880-b897-11ea-8ce9-078713020a7d.PNG">

```SQL
-- 셀프조인을 이용한 풀이
SELECT T1.YYYYMM, T1.AMT
    , SUM(CASE WHEN T2.YYYYMM < T1.YYYYMM THEN T2.AMT END) PRE_3SUM
    , SUM(CASE WHEN T2.YYYYMM > T1.YYYYMM THEN T2.AMT END) FOL_3SUM
    FROM T T1, T T2
  WHERE T2.YYYYMM >= TO_CHAR(ADD_MONTHS(TO_DATE(T1.YYYYMM,'YYYYMM'),-3),'YYYYMM')
    AND
        T2.YYYYMM <= TO_CHAR(ADD_MONTHS(TO_DATE(T1.YYYYMM,'YYYYMM'),3),'YYYYMM')
  GROUP BY T1.YYYYMM, T1.AMT
  ORDER BY T1.YYYYMM


```


복습완료 2021.07.13
</BR>
복습완료 2022.03.04
