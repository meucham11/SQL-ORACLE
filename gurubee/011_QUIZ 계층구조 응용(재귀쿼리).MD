출처 : http://www.gurubee.net/lecture/2250

----

```
재귀커리를 짜는 것이다
재귀 커리안에 START WITH ENAME= E.ENAME으로 짰었는데
이 경우에는 이름이 중복되었을 때 문제가 발생한다
```

```SQL
SELECT EMPNO
    , LEVEL LV
    , LPAD(ENAME, LENGTH(ENAME)+(LEVEL-1)*2,' ') ENAME
    , SUBSTR(SYS_CONNECT_BY_PATH(ENAME,'-'),2) ENAMES
    , SAL
    , (SELECT SUM(SAL)
            FROM EMP
          START WITH EMPNO = E.EMPNO
          CONNECT BY PRIOR EMPNO = MGR
       ) SUM_SAL
    FROM EMP E
  START WITH MGR IS NULL
  CONNECT BY PRIOR EMPNO = MGR
  ORDER SIBLINGS BY EMPNO ;
 
```
