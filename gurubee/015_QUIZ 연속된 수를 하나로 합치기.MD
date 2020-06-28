출처 : http://www.gurubee.net/lecture/2834

----

### 1단계 연속한 숫자 합치기
```SQL
SELECT CHA, MIN(LV), MAX(LV), COUNT(*)
    , MIN(LV) || DECODE(COUNT(*),1,'','~'||MAX(LV)) V
    FROM(SELECT LV
        , LV - ROWNUM CHA
        FROM T)
    GROUP BY CHA
    ORDER BY CHA;
```
<img width="203" alt="1" src="https://user-images.githubusercontent.com/34879309/85935347-c601e780-b92a-11ea-877b-6badf430b65c.PNG">


### 2단계 총 4개의 열에 연속한 숫자 합치고, 연속된 숫자의 갯수가 5개가 안되면 따로 쓰기
```
GROUP BY를 이렇게 작성하는 것을 처음 봄.
```
```SQL
SELECT 
     MIN(DECODE(MOD(ROWNUM-1,4),0,V)) V1
    , MIN(DECODE(MOD(ROWNUM-1,4),1,V)) V2
    , MIN(DECODE(MOD(ROWNUM-1,4),2,V)) V3
    , MIN(DECODE(MOD(ROWNUM-1,4),3,V)) V4
    FROM(SELECT CHA CHA_1
        , CNT_CHA
        , CASE WHEN CNT_CHA<5 THEN LV END CHA_2
        , MIN(LV) || DECODE(COUNT(*), 1, '', '~'||MAX(lv)) v
        FROM(SELECT LV,CHA
            , MIN(LV) OVER(PARTITION BY CHA ORDER BY LV 
                            ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) FROM_LV
            , MAX(LV) OVER(PARTITION BY CHA ORDER BY LV 
                            ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) TO_LV
            , COUNT(LV) OVER(PARTITION BY CHA) CNT_CHA 
                FROM(SELECT LV
                    , LV - ROWNUM CHA
                    FROM T))
      GROUP BY CHA, CNT_CHA, CASE WHEN CNT_CHA<5 THEN LV END
      ORDER BY MIN(LV)
      )
      GROUP BY CEIL(ROWNUM/4)
      ORDER BY CEIL(ROWNUM/4)
;

```
<img width="129" alt="1" src="https://user-images.githubusercontent.com/34879309/85936320-804a1c80-b934-11ea-98e3-9592a57d2606.PNG">


### 해답코드
```SQL
SELECT MIN(DECODE(MOD(rn, 4), 1, v)) v1
     , MIN(DECODE(MOD(rn, 4), 2, v)) v2
     , MIN(DECODE(MOD(rn, 4), 3, v)) v3
     , MIN(DECODE(MOD(rn, 4), 0, v)) v4
  FROM (SELECT ROW_NUMBER() OVER(ORDER BY MIN(lv)) rn
             , MIN(lv) || DECODE(COUNT(*), 1, '', '~'||MAX(lv)) v
          FROM (SELECT lv
                     , ROWNUM rn
                     , lv - ROWNUM grp
                     , COUNT(*) OVER(PARTITION BY lv - ROWNUM) cnt
                  FROM (SELECT lv FROM t ORDER BY lv)
               )
         GROUP BY grp, CASE WHEN cnt < 5 THEN lv END
       )
 GROUP BY CEIL(rn / 4)
 ORDER BY CEIL(rn / 4)
;

```

|1단계|2단계 |3단계|4단계|
| ---------- | :--------- | :----------: | ----------: |
|<img width="33" alt="1" src="https://user-images.githubusercontent.com/34879309/85936360-dfa82c80-b934-11ea-8989-cc1894ed21e1.PNG">|<img width="92" alt="2" src="https://user-images.githubusercontent.com/34879309/85936361-e040c300-b934-11ea-8d51-3c31bf9e5dfe.PNG">|<img width="67" alt="3" src="https://user-images.githubusercontent.com/34879309/85936362-e171f000-b934-11ea-9427-da85953c548e.PNG">|<img width="130" alt="4" src="https://user-images.githubusercontent.com/34879309/85936363-e20a8680-b934-11ea-91cf-d7d002569a38.PNG">|
