출처 : http://www.gurubee.net/lecture/2912

----

```SQL
SELECT CONNECT_BY_ROOT(ID) GR_ID
      ,LEVEL SEQ
      ,SUBSTR(SYS_CONNECT_BY_PATH(ID,'-'),2) PATH
    FROM T
  START WITH NOT EXISTS(SELECT 1
                                  FROM T A
                                WHERE T.S_X = A.E_X
                                  AND T.S_Y = A.E_Y
                                  AND T.S_Z = A.E_Z
                              )
  CONNECT BY PRIOR E_X = S_X
         AND PRIOR E_Y = S_Y
         AND PRIOR E_Z = S_Z
  ORDER SIBLINGS BY ID;
  ```
