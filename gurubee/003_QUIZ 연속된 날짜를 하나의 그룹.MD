# 연속된 날짜를 하나의 그룹으로 표현해 보자
출처 : http://www.gurubee.net/lecture/2194

#### 내 코드
```SQL
SELECT NO, MIN(DT) FROM_DT, MAX(DT) TO_DT, COUNT(*)CNT
    FROM(
        SELECT NO, DT,
               SUB,
               SUM(SUB) OVER(PARTITION BY NO ORDER BY DT) GRP
               FROM(
                    SELECT NO, DT,
                           DECODE(TO_DATE(DT,'yyyymmdd')-TO_DATE(LG,'yyyymmdd'),1,0,1) SUB
                        FROM(
                            SELECT NO, DT, 
                                   NVL(LAG(DT) over(PARTITION BY NO ORDER BY DT),DT) LG
                            FROM T
                        ) SUB_T
                    )
        )
  GROUP BY NO, GRP
  ORDER BY NO,FROM_DT;
```


#### 해답
```sql
SELECT NO,
       MIN(DT) FROM_DT,
       MAX(DT) TO_DT,
       COUNT(*) CNT
    FROM (SELECT * FROM T ORDER BY NO, DT)
    GROUP BY NO, TO_DATE(DT, 'yyyymmdd') - ROWNUM
```

복습 완료 </br>
복습 완료2
