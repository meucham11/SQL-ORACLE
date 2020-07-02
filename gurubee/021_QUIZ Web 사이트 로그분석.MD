출처 : http://www.gurubee.net/lecture/2864

----

```SQL
CREATE TABLE web_log
AS
SELECT '111' id, 'www.gurubee.net' site, '11:10' TM FROM DUAL
UNION ALL SELECT '111', 'www.gurubee.net', '11:11' FROM DUAL
UNION ALL SELECT '111', 'www.imaso.co.kr', '11:12' FROM DUAL
UNION ALL SELECT '111', 'www.imaso.co.kr', '11:13' FROM DUAL
UNION ALL SELECT '111', 'www.gurubee.net', '11:14' FROM DUAL
UNION ALL SELECT '222', 'www.gurubee.net', '11:11' FROM DUAL
UNION ALL SELECT '222', 'www.imaso.co.kr', '11:12' FROM DUAL
UNION ALL SELECT '222', 'www.imaso.co.kr', '11:13' FROM DUAL
UNION ALL SELECT '222', 'www.imaso.co.kr', '11:14' FROM DUAL
;
```

