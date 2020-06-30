출처 : http://www.gurubee.net/lecture/2837

----

```
16번 퀴즈랑 같은 원리인데 음.. 아직 잘 모르겠다. 2020/06/29
깨달음 2020/06/30
```

----

```SQL
SELECT A.CD
      ,A.ID
      ,LEAST(A.CNT
            ,B.CNT
            ,A.S_CNT - (B.S_CNT-B.CNT)
            ,B.S_CNT - (A.S_CNT-A.CNT)
            ) CNT
       ,B.ID
    FROM (SELECT A.*, SUM(CNT) OVER(PARTITION BY CD ORDER BY DT) S_CNT FROM SUJU A) A,
         (SELECT B.*, SUM(CNT) OVER(PARTITION BY CD ORDER BY DT) S_CNT FROM IPGO B) B
  WHERE A.CD=B.CD
    AND A.S_CNT > B.S_CNT-B.CNT
    AND B.S_CNT > A.S_CNT-A.CNT
  ORDER BY A.CD, A.DT, B.DT
```
