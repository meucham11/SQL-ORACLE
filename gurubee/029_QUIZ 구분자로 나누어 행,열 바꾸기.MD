출처 : http://www.gurubee.net/lecture/2956
----

CREATE TABLE t
AS
SELECT 1 no, '1:10|2:11|3:12|4:15' v FROM dual
UNION ALL SELECT 2, '1:17|3:15|4:25' FROM dual
UNION ALL SELECT 3, '2:11|4:15'      FROM dual
UNION ALL SELECT 4, '1:10|2:21|4:19' FROM dual;
 
SELECT * FROM t;

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
