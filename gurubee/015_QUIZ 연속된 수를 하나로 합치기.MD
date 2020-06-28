출처 : http://www.gurubee.net/lecture/2834

----

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

```SQL


```
