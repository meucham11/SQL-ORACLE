출처 : http://www.gurubee.net/lecture/2956
----

```SQL
SELECT *
FROM(
    SELECT no
         , SUBSTR(REGEXP_SUBSTR(v, '1:[^|]+'), 3) v1
         , SUBSTR(REGEXP_SUBSTR(v, '2:[^|]+'), 3) v2
         , SUBSTR(REGEXP_SUBSTR(v, '3:[^|]+'), 3) v3
         , SUBSTR(REGEXP_SUBSTR(v, '4:[^|]+'), 3) v4
      FROM t
    )  
    UNPIVOT (V FOR GB IN(V1,V2,V3,V4))
    PIVOT(MIN(V) FOR NO IN(1,2,3,4))
;
```
