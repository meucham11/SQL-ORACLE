# MySQL
## cmd에서 구동

### 1. 설치하기
https://dev.mysql.com/downloads/mysql/  OS환경에 따라 설치해주자.
공식홈페이지에서는 조금 까다롭기 때문에
bitnami wamp 구글 검색 후 https://bitnami.com/stack/wamp 링크에서 최근거 받아줌. 로그인 필요없음
 
설치후
c드라이브 / bitnami / mysql / manager-windows.exe를 실행해주면 된다.
실행 후 Manage Servers를 보면 MySQL이 켜져있는 것을 볼 수 있다.

시작 cmd를 켠다.
cd C:\Bitnami\wampstack-7.3.11-0\mysql\bin
mysql -uroot -p
패스워드입력 엔터

mysql>  로 뜨면 성공
