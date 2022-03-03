출처 : http://www.gurubee.net/lecture/2223

----

```
조인같은걸 할줄 알았는데 함수가 있었다.
SELECT 절에 PRIOR과 SYS_CONNECT_BY_PATH
```

```SQL
SELECT EMPNO, ENAME, LEVEL, MGR
    , PRIOR ENAME MGR_ENAME
    , SUBSTR(SYS_CONNECT_BY_PATH(ENAME,'-'),2) ENAMES
    FROM EMP
  START WITH MGR IS NULL
  CONNECT BY PRIOR EMPNO = MGR
  ORDER SIBLINGS BY EMPNO
```
<img width="333" alt="캡처1" src="https://user-images.githubusercontent.com/34879309/85370905-6a221200-b56a-11ea-9579-bfc1501499e6.PNG">



복습완료 21.06.29
복습완료 22.03.03
