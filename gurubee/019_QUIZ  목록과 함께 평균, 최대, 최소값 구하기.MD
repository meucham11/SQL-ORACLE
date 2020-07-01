출처 : http://www.gurubee.net/lecture/2862

----

```
개어렵네
```

```SQL
--1단계 
--여기까지 뽑아야 과정이 어떻게 되는지 살펴보기 쉬울듯
SELECT DT
      ,AVG(V1)
      ,AVG(V2)
      ,AVG(V3)
      ,AVG(V4)
      ,YN
      ,GROUP_ID() GID
      ,GROUPING(YN) G_YN
      ,GROUPING(DT) G_DT
      ,GROUPING_ID(YN,DT) GPING_ID
    FROM T
  GROUP BY 1,ROLLUP(1,1,YN,1,1,DT)
  HAVING NOT(YN='N' AND GROUPING_ID(YN,DT)=1)
  ORDER BY DT,YN,GID
```


```SQL
--2단계 : 계산
```
