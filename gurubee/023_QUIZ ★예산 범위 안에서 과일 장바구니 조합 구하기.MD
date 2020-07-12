출처 : http://www.gurubee.net/lecture/2878

---

```
어렵누..
```


```SQL
WITH t1(cod, nam, amt, cnt, nams, amts, tot) AS
(
SELECT cod, nam, amt
     , 1 cnt
     , CAST(nam AS VARCHAR2(4000)) nams
     , CAST(amt AS VARCHAR2(4000)) amts
     , amt tot
  FROM t
 WHERE amt < = 5000
 UNION ALL
SELECT c.cod, c.nam, c.amt
     , DECODE(p.cod, c.cod, p.cnt+1, 1) cnt
     , DECODE(p.cod, c.cod,
 REGEXP_REPLACE(p.nams,'[*][0-9]+$')||'*'||(p.cnt+1)
       , p.nams||'+'||c.nam) nams
     , DECODE(p.cod, c.cod,
 REGEXP_REPLACE(p.amts,'[*][0-9]+$')||'*'||(p.cnt+1)
       , p.amts||'+'||c.amt) amts
     , p.tot + c.amt tot
  FROM t  c
     , t1 p
 WHERE p.tot + c.amt < = 5000
   AND p.cod < = c.cod
)
SELECT nams, amts
  FROM t1
 WHERE tot = 5000
;
```
