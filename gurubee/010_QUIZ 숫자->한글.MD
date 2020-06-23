출처 : http://www.gurubee.net/lecture/2224

----

```SQL
CREATE TABLE t 
    AS
SELECT 123456789012345 amt FROM dual
 UNION ALL SELECT 29000 FROM dual
 UNION ALL SELECT 309840 FROM dual
;
 
SELECT AMT,V
    , TRANSLATE(
      SUBSTR(V,1,1)||DECODE(SUBSTR(V,1,1),0,'','천')
    || SUBSTR(V,2,1)||DECODE(SUBSTR(V,2,1),0,'','백')
    || SUBSTR(V,3,1)||DECODE(SUBSTR(V,3,1),0,'','십')
    || SUBSTR(V,4,1)||DECODE(SUBSTR(V,4,1),0,'','조')
    ||  SUBSTR(V,5,1)||DECODE(SUBSTR(V,5,1),0,'','천')
    || SUBSTR(V,6,1)||DECODE(SUBSTR(V,6,1),0,'','백')
    || SUBSTR(V,7,1)||DECODE(SUBSTR(V,7,1),0,'','십')
    || SUBSTR(V,8,1)||DECODE(SUBSTR(V,8,1),0,'','억')
    ||  SUBSTR(V,9,1)||DECODE(SUBSTR(V,9,1),0,'','천')
    || SUBSTR(V,10,1)||DECODE(SUBSTR(V,10,1),0,'','백')
    || SUBSTR(V,11,1)||DECODE(SUBSTR(V,11,1),0,'','십')
    || SUBSTR(V,12,1)||DECODE(SUBSTR(V,12,1),0,'','만')
    ||  SUBSTR(V,13,1)||DECODE(SUBSTR(V,13,1),0,'','천')
    || SUBSTR(V,14,1)||DECODE(SUBSTR(V,14,1),0,'','백')
    || SUBSTR(V,15,1)||DECODE(SUBSTR(V,15,1),0,'','십')
    || SUBSTR(V,16,1)
    , '1234567890','일이삼사오육칠팔구'
    ) TRL
    FROM (SELECT AMT, LPAD(AMT,16,'0') V FROM T)
;
```
