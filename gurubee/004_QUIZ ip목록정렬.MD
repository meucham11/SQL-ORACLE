출처 : http://www.gurubee.net/lecture/2195

```SQL
SELECT ROWNUM RN,
       IP
       FROM(
            SELECT ROWNUM RM,
            IP,
            LPAD(ST1,3,'0') D1,
            LPAD(ST2,3,'0') D2,
            LPAD(ST3,3,'0') D3,
            LPAD(ST4,3,'0') D4
                FROM(
                    SELECT ROWNUM RN,
                           IP,
                           SUBSTR(IP,1,INSTR(IP, '.', 1,1)-1) AS ST1,
                           SUBSTR(IP,INSTR(IP, '.', 1,1)+1,
                                  INSTR(IP, '.',1,2)-INSTR(IP, '.',1,1)-1) AS ST2,
                           SUBSTR(IP,INSTR(IP, '.', 1,2)+1,
                                  INSTR(IP, '.',1,3)-INSTR(IP, '.',1,2)-1) AS ST3,
                           SUBSTR(IP,INSTR(IP, '.', 1,3)+1,LENGTH(IP)) AS ST4
                        FROM T)
        )
  ORDER BY D1,D2,D3,D4;
```

복습완료
</BR>
복습완료2
```SQL
SELECT ROWNUM RN
      ,REGEXP_REPLACE(REPLACE('.'||IP,'.','.00'),'([^.]{3}(\.|$))|.','\1') D1
    FROM T
    ORDER BY D1
```
