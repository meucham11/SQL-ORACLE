출처 : http://www.gurubee.net/lecture/2836

----

```
꿀잼
```

```SQL
-- 갯수세기
SELECT 
  NVL(X1, SUM(X1_BOMB) OVER(ORDER BY 1 ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)) ANW_1
 ,NVL(X2, SUM(X2_BOMB) OVER(ORDER BY 1 ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)) ANW_2
 ,NVL(X3, SUM(X3_BOMB) OVER(ORDER BY 1 ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)) ANW_3
 ,NVL(X4, SUM(X4_BOMB) OVER(ORDER BY 1 ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)) ANW_4
 ,NVL(X5, SUM(X5_BOMB) OVER(ORDER BY 1 ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)) ANW_5
    FROM(-- 좌표에 나타내기 
        SELECT Y,X1,X2,X3,X4,X5
              ,NVL(LENGTH(X1||X2),0) X1_BOMB
              ,NVL(LENGTH(X1||X2||X3),0) X2_BOMB
              ,NVL(LENGTH(X2||X3||X4),0) X3_BOMB
              ,NVL(LENGTH(X3||X4||X5),0) X4_BOMB
              ,NVL(LENGTH(X4||X5),0) X5_BOMB
            FROM(-- 랜덤 10개에 *표시
                  SELECT Y
                      ,MIN(DECODE(X,1,CH)) X1
                      ,MIN(DECODE(X,2,CH)) X2
                      ,MIN(DECODE(X,3,CH)) X3
                      ,MIN(DECODE(X,4,CH)) X4
                      ,MIN(DECODE(X,5,CH)) X5
                    FROM(--좌표생성
                        SELECT CEIL(LEVEL/5) X 
                              ,MOD(LEVEL-1,5)+1 Y
                              ,CASE WHEN ROW_NUMBER() OVER(ORDER BY DBMS_RANDOM.RANDOM())<=10
                                THEN '*' END CH
                            FROM DUAL
                          CONNECT BY LEVEL<=25
                          ORDER BY X,Y
                        )
                  GROUP BY Y
                )
        )
```

|1단계|2단계|3단계|4단계|5단계|
|---:|---:|---:|---:|---:|
|<img width="47" alt="1" src="https://user-images.githubusercontent.com/34879309/85977286-4f8ee380-ba17-11ea-8db7-54fec2065cb7.PNG">|<img width="63" alt="2" src="https://user-images.githubusercontent.com/34879309/85977421-8cf37100-ba17-11ea-9552-eab7d0f8c7d0.PNG">|<img width="112" alt="3" src="https://user-images.githubusercontent.com/34879309/85977424-8e249e00-ba17-11ea-8448-3e6400171d3e.PNG">|<img width="340" alt="4" src="https://user-images.githubusercontent.com/34879309/85977427-8f55cb00-ba17-11ea-811d-87cdf3181960.PNG">|<img width="199" alt="5" src="https://user-images.githubusercontent.com/34879309/85977429-9086f800-ba17-11ea-881f-24ceddb884c1.PNG">|



복습완료 2021.07.15 </br>
복습완료 2022.03.20
