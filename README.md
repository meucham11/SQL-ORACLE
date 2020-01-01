# MySQL
## cmd에서 구동

### 1. 설치하기
https://dev.mysql.com/downloads/mysql/  OS환경에 따라 설치해주자.
공식홈페이지에서는 조금 까다롭기 때문에
bitnami wamp 구글 검색 후 https://bitnami.com/stack/wamp 링크에서 최근거 받아줌. 로그인 필요없음
 
설치후
c드라이브 / bitnami / mysql / manager-windows.exe를 실행해주면 된다.
실행 후 Manage Servers를 보면 MySQL이 켜져있는 것을 볼 수 있다. (다음에는 켜주면 된다.)

초록불을 확인 했다면 
시작-cmd
cd C:\Bitnami\wampstack-7.3.11-0\mysql\bin
mysql -uroot -p
패스워드입력 엔터

mysql>  로 뜨면 성공


## 1.  데이터베이스의 개념
DB : 자료, 대상을 모아논 것
DBMS : 자료를 관리하는 프로그램 
응용 프로그램을 통해 DBMS를 작동시켜 DB에 접근한다.


## 2. 데이터베이스의 특징
### 통합된 데이터
  - 데이터를 통합하는 개념
  - 각자 사용하던 데이터의 중복을 최소화하여 중복으로 인한 데이터 불일치현상 제거
### 저장된 데이터
  - 문서로 보관된 데이터가 아니라 디스크, 테이프 같은 저장장치에 저장된 데이터
### 운영 데이터
  - 조직의 목적을 위해 사용되는 데이터
  - 업무를 위한 검색을 할 목적으로 저장된 데이터
### 공용 데이터
  - 공동으로 사용되는 데이터
  
## 3. 데이터베이스의 장점
 - 데이터 중복읭 최소화
 - 데이터의 공용
 - 일관성 유지
 - 무결성 유지
 - 보안 보장
 - 표준화 용이
 - 전체 데이터 요구의 조정
 
 
## 4. DBMS 제품
 - Oracle : RDMS 최초 상용화, RDBMS 시장 점유윺 높음
 - IBM DB2 : RDBMS 최초개발, 메인프레임 등에서 점유율 높음
 - MS-SQL'Server : Sybase 코드에 기반
 - 기타 : Teradata, Informix, Sybase
          MySQL, Cubrid etc...

## 5. 관계형 데이터베이스의 특징
 - 2차원 테이블로 표현
 - 데이터 무결성
 - 데이터 처리를 위해 SQL 사용
 - 한 번에 레코드를 처리하는 것이 아니라 집합을 처리함

 
