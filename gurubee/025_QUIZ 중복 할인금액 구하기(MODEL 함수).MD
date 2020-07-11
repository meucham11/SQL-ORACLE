출처 : http://www.gurubee.net/lecture/2881

----

```
내풀이
AUTOMATIC ORDER하나 빼먹어서 생고생했네...
```

```SQL
SELECT *
    FROM T
  MODEL
  DIMENSION BY (SEQ)
  MEASURES(AMT, RAT, 20000 PRC, 0 DC, 0 VAL)
  RULES AUTOMATIC ORDER(
        PRC[ANY] = NVL(VAL[CV()-1],PRC[1])
       ,VAL[ANY] = DECODE(RAT[CV()],NULL,PRC[CV()]-AMT[CV()],PRC[CV()]*(100-RAT[CV()])/100)
       ,DC[ANY] = PRC[CV()]-VAL[CV()]
        );
```
<img width="175" alt="1" src="https://user-images.githubusercontent.com/34879309/86752559-67e7a980-c07a-11ea-92b9-a0dd1a7738f7.PNG">


```SQL
SELECT *
  FROM t
 MODEL
 DIMENSION BY (seq)
 MEASURES (amt, rat, 20000 prc, 0 dc, 0 rem)
 RULES
 ( rem[ANY] = NVL( rem[CV()-1], prc[1])
            - NVL( amt[CV()]
                 , NVL(rem[CV()-1], prc[1])
                   * rat[CV()] / 100
                 )
 , prc[seq > 1] = rem[CV()-1]
 , dc[ANY] = prc[CV()] - rem[CV()]
 )
;
```
