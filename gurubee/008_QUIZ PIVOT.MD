출처 : http://www.gurubee.net/lecture/2214
----


```SQL
WITH t AS
(
SELECT CHR(LEVEL + 64) c
     , LEVEL v
  FROM dual
CONNECT BY LEVEL <= 26
)
SELECT DECODE(GB2,1,C,V) V, 
       CEIL(V/7) GB1,
       LV.GB2,
       MOD(V-1,7)+1 GB3
    FROM t, (SELECT LEVEL GB2 FROM DUAL CONNECT BY LEVEL <=2) LV
;
```
<img width="93" alt="캡처1" src="https://user-images.githubusercontent.com/34879309/85366819-0ea05600-b563-11ea-8fea-2724b641a448.PNG">

```SQL
WITH t AS
(
SELECT CHR(LEVEL + 64) c
     , LEVEL v
  FROM dual
CONNECT BY LEVEL <= 26
)
SELECT GB1, GB2,
    DECODE(GB3,1,V) GB3
    --MIN(DECODE(GB3,1,V)) GB3
    FROM(
        SELECT DECODE(GB2,1,C,V) V, 
               CEIL(V/7) GB1,
               LV.GB2,
               MOD(V-1,7)+1 GB3
            FROM t, (SELECT LEVEL GB2 FROM DUAL CONNECT BY LEVEL <=2) LV
        )
   -- GROUP BY GB1,GB2
    --ORDER BY GB1,GB2
;
```
<img width="81" alt="캡처2" src="https://user-images.githubusercontent.com/34879309/85366824-0fd18300-b563-11ea-9ef9-2ed2a0455d4f.PNG">

```SQL
WITH t AS
(
SELECT CHR(LEVEL + 64) c
     , LEVEL v
  FROM dual
CONNECT BY LEVEL <= 26
)
SELECT GB1, GB2,
      MIN(DECODE(gb3, 1, v)) v1
    , MIN(DECODE(gb3, 2, v)) v2
    , MIN(DECODE(gb3, 3, v)) v3
    , MIN(DECODE(gb3, 4, v)) v4
    , MIN(DECODE(gb3, 5, v)) v5
    , MIN(DECODE(gb3, 6, v)) v6
    , MIN(DECODE(gb3, 7, v)) v7
    FROM(
        SELECT DECODE(GB2,1,C,V) V, 
               CEIL(V/7) GB1,
               LV.GB2,
               MOD(V-1,7)+1 GB3
            FROM t, (SELECT LEVEL GB2 FROM DUAL CONNECT BY LEVEL <=2) LV
        )
   GROUP BY GB1,GB2
   ORDER BY GB1,GB2
;
```
<img width="168" alt="캡처3" src="https://user-images.githubusercontent.com/34879309/85366828-106a1980-b563-11ea-9586-16904aba291b.PNG">


----
****피봇 이용

```SQL
--음.. 잘 이해가 되질 않는구만 

WITH t AS
(
SELECT CHR(LEVEL + 64) c
     , LEVEL v
  FROM dual
CONNECT BY LEVEL <= 26
)
SELECT *
    FROM(SELECT *
            FROM(SELECT C, TO_CHAR(V) V, CEIL(V/7) GB1, MOD(V-1,7)+1 GB3
                    FROM T
            ) UNPIVOT(V FOR GB2 IN (C AS 1, V AS 2))
    )PIVOT(MIN(V) FOR GB3 IN (1 V1, 2 V2, 3 V3, 4 V4, 5 V5,6 V6, 7 V7))
ORDER BY 1,2
;
```
