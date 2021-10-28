# 개요
본 자료는 Redis의 기본 Architecture 및 library 기능을 분석하기 위해 작성되었습니다.

# Redis
## <strong>설명</strong>
레디스(Redis)는 Remote Dictionary Server의 약자로서[3], "키-값" 구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 비관계형 데이터베이스 관리 시스템(DBMS)이다. 2009년 살바토르 산필리포(Salvatore Sanfilippo)가 처음 개발했다. 2015년부터 Redis Labs가 지원하고 있다. 모든 데이터를 메모리로 불러와서 처리하는 메모리 기반 DBMS이다. BSD 라이선스를 따른다
## <strong>Architecture</strong>
### Redis Topology
Redis는 Master-Slave 형태로 구성할 수 있으며 데이터를 복제해서 운영할 수 있다. master-slave간 복제는 non-blocking 상태로 이루어진다.
### Redis Sharding
레디스에서 데이터를 샤딩하여 레디스의 read 성능을 높일 수 있다. 예를 들어 #1~#999, #1000~#1999ID 형태로 데이터를 나누어서 데이터의 용량을 확장하고 각 서버에 있는 Redis의 부하를 나누어 줄일 수 있다.
### Redis Cluster
Redis는 Single Instance로서 사용할 때 Sharding이나 Topology로서 커버해야 했던 부분을 Clustering을 이용함으로서 어플리케이션을 설계하는 데 좀 더 수월해졌다.
## <strong>Data Model</strong>
### <strong>String</strong>
Value에는 문자,숫자 등을 저장한다. 저장 시 별도로 형이 없다. 그리고 숫자에 연산기능도 가능해서 특정 수를 더하거나 뺄 수 있다.  
ex) incrby "test_key" 10
### <strong>Lists</strong>
Value에 list를 저장한다. 중복이 허용된다.
### <strong>Sets</strong>
Value에 Set형태를 가지고 있으며, list와 다른 점은 중복이 허용되지 않는다.
### <strong>Hashes</strong>
Value를 Hash형태로 가지고 있다.
### <strong>Sorted set</strong>
value를 set형태로 가지고 있으며 score와 함께 저장되며 이를 기준으로 정렬된다.
### <strong>Bitmaps</strong>
bit값을 저장한다.
## <strong>사용용도</strong>
* Message Queue
* Shared Memory
* Remote dictionary

## <strong>지원 언어</strong>
* Java
* Python
* Node.js
* .Net
* Go
## <strong>library</strong>
### <strong>Java</strong>
보편적으로 많은 쓰는 Java library로는 Jedis와 Lettuce가 있으며 모두 오픈소스 이다. 최근에는 lettuce를 쓰며 spring boot에도 lettuce가 기본 의존성으로 등록 되어있다. lettuce는 netty 기반의 redis 클라이언트이며, 비동기로 요청을 처리하기 때문에 Jedis보다 고성능을 지원한다.
## <strong>보안</strong>
