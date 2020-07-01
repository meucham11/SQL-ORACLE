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
<img width="364" alt="1" src="https://user-images.githubusercontent.com/34879309/86196562-758ac400-bb8e-11ea-8b0e-4257548a085c.PNG">

```SQL
--2단계 : 계산
SELECT DT
      ,DECODE(GROUP_ID(),0,AVG(V1),1,MAX(V1),2,MIN(V1)) V1
      ,DECODE(GROUP_ID(),0,AVG(V2),1,MAX(V2),2,MIN(V2)) V1
      ,DECODE(GROUP_ID(),0,AVG(V3),1,MAX(V3),2,MIN(V3)) V3
      ,DECODE(GROUP_ID(),0,AVG(V4),1,MAX(V4),2,MIN(V4)) V4
      ,YN
      ,GROUP_ID() GID
      ,GROUPING(YN) G_YN
      ,GROUPING(DT) G_DT
      ,GROUPING_ID(YN,DT) GPING_ID
    FROM T
  GROUP BY 1, ROLLUP(1,1,YN,1,1,DT)
  HAVING NOT(YN='N' AND GROUPING_ID(YN,DT)=1)
  ORDER BY DT,YN,GID
```
<img width="279" alt="2" src="https://user-images.githubusercontent.com/34879309/86196565-76235a80-bb8e-11ea-89a8-abe4a6ca1ee3.PNG">


```SQL
-- DT 빈칸 채워주기
SELECT NVL(dt, NVL(yn, '전체') ||' '||
       DECODE(GROUP_ID(), 0, '평균값', 1, '최대값', 2, '최소값')) dt
      ,DECODE(GROUP_ID(),0,AVG(V1),1,MAX(V1),2,MIN(V1)) V1
      ,DECODE(GROUP_ID(),0,AVG(V2),1,MAX(V2),2,MIN(V2)) V1
      ,DECODE(GROUP_ID(),0,AVG(V3),1,MAX(V3),2,MIN(V3)) V3
      ,DECODE(GROUP_ID(),0,AVG(V4),1,MAX(V4),2,MIN(V4)) V4
      ,YN
      ,GROUP_ID() GID
      ,GROUPING(YN) G_YN
      ,GROUPING(DT) G_DT
      ,GROUPING_ID(YN,DT) GPING_ID
    FROM T
  GROUP BY 1, ROLLUP(1,1,YN,1,1,DT)
  HAVING NOT(YN='N' AND GROUPING_ID(YN,DT)=1)
  ORDER BY DT,YN,GID
```
<img width="282" alt="3" src="https://user-images.githubusercontent.com/34879309/86196568-76bbf100-bb8e-11ea-9a16-738137411fa5.PNG">

```SQL
-- 피봇/언피봇 이용
SELECT NVL(dt, NVL(yn, '전체') ||' '||
       DECODE(gid, 0, '평균값', 1, '최대값', 2, '최소값')) dt
     , v1, v2, v3, v4
     , yn
  FROM (SELECT gb, yn, dt
             , DECODE(GROUP_ID(), 0, ROUND(AVG(v), 2), 1, MAX(v), 2, MIN(v)) v
             , GROUP_ID() gid
          FROM t
         UNPIVOT (v FOR gb IN (v1, v2, v3, v4))
         GROUP BY gb, 1, ROLLUP(1, 1, yn, 1, 1, dt)
         HAVING NOT (yn = 'N' AND GROUPING_ID(yn, dt) = 1)
        )
 PIVOT (MIN(v) FOR gb IN ('V1' AS v1, 'V2' AS v2, 'V3' AS v3, 'V4' AS v4)) a
 ORDER BY a.dt, a.yn, a.gid
;

```
