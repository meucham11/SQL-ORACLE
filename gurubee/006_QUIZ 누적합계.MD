출처 : http://www.gurubee.net/lecture/2203

-------------------------------------------------
```SQL
CREATE TABLE t AS
    SELECT 1 seq, -2000 amt FROM dual
    UNION ALL SELECT 2, 4000 FROM dual
    UNION ALL SELECT 3, -5000 FROM dual
    UNION ALL SELECT 4, -2000 FROM dual
    UNION ALL SELECT 5, 3000 FROM dual
    UNION ALL SELECT 6, 1500 FROM dual
    UNION ALL SELECT 7, -250 FROM dual
    UNION ALL SELECT 8, 320 FROM dual
    UNION ALL SELECT 9, -4000 FROM dual
    UNION ALL SELECT 10, 10000 FROM dual
    UNION ALL SELECT 11, -20000 FROM dual
;


-- 기본적인 누적합계
SELECT SEQ, AMT,
    SUM(AMT) OVER(ORDER BY SEQ) RESULT
    FROM T
    
-- 문제에 맞게 음수인 것들은 0처리
SELECT SEQ, AMT,
    SUM(AMT) OVER(ORDER BY SEQ) RESULT,
    GREATEST(0 ,SUM(AMT) OVER(ORDER BY SEQ)) RESULT_2
    FROM T

--위와같이 할 경우 절차적인 주행방식이 아니므로 MODEL을 사용하자 PL/SQL을 쓴느것도 정답
- MODEL : MODEL 기능을 사용하겠다고 선언하는 부분입니다.
- DIMENSION BY (seq) : 레코드를 구별하는 키를 선언하는 부분입니다.
- MEASURES (amt, 0 result) : 키가 아닌 다른 항목들을 표시합니다.
- RULES () : 여기서는 배열 구조의 값을 지정하는 구문입니다.


```
