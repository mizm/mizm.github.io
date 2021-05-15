# Redis
## 소개
- In-Memory Data Structure Store
- Open Source
- Support adata structures
    - String, set, sorted-sert hashes, list
    - bitmap, geospatial index
    - stream
- Only 1 Committer
## Cache
- 나중에 요청의 결과를 빠르게 보여주기 위함
- 접근 속도가 다름 디스크 < 메모리
- Look aside Cache
    - web server에서 캐시를 확인
    - 캐시에 없으면 디비에서 확인 후 캐시에 추가
- Write Back
    - 쓰기가 많은 경우
    - Cache에 특정 시간동안 저장
    - Cache에 있는 데이터를 Dbdㅔ 저장한다
    - Db에 저장된 데이터를 삭제한다.

## Collection 이 중요한지
- 개발의 편의성
    - 랭킹서버
    - Redis의 sorted- set 이용하면 바로 가능
- 개발의 난이도
    - 친구 리스트 key /value 형태로 저장해야함
    - 레디스의 자료구조는 Atomic하기 때문에 Race Condition을 피할 수 있씁니당 -> 잘못짜면 망함
- 개발 시간을 단축시키고 개발 편의성이 좋음

## 사용처
- remote data source
    - a서버 , B서버, C서버에서 데이터를 공유
    - Redis가 자체가 Atomic 을 보장해준다.
- 인증 토큰 등을 저장
- Ranking 보드로 사용
- 유저 API Limit
- 잡 큐 (list)

## Collection
- String
    - 단일 key
    -aajfxlzl
- list
    - lpush <key> <A>
    - Rpush <key> <B>
    - LPOP, RPOP
- Set
    - SADD
    - SMEMBERS
    - SISMEMBERS
- Sorted Set : 정렬이 되는 Set
    - ZADD <key> <Sorce> <Value>
    - ZRANGE <KEY> <Start> <End>
    - score는 double 타입임 자바 스크립트에서는 큰 숫자는 Long으로 보내는게 아니고 String으로 보내야함
- Hash : Key 밑에 sub Key가 존재한다

## Redis 운영
- 메모리 관리를 잘하자
    - Physical Memory 이상을 사용하면 문제가 발생
        - swap 있다면 해당 메모리 page 마다 접근시 늦어짐
        - disk 에 저장하기 떄문
    - MaxMemory를 설정하더라도 이보다 더 사용할 가능성이 큼
        - 메모리는 페이지 처리로 할당
        - 파편화가 생길 수 있음
    - RSS 모니터링 확인
    - 현재 메모리를 사용해서 Swap을 쓰고 있다는 것 을 모름
    - 적은 메모리를 사용하는 여러개가 안전하다
    - 다양한 사이즈를 가지는 데이터 보다는 유사한 데이터 사이즈가 유리하다.
    - 좀 더 메모리 많은 장비로 Migration
    - 있는 데이터 줄이기 > 벌써 swap 중이면 프로세스를 재시작 해야함.
    - 자료구조들은 메모리를 많이 사용함.
        - hash -> hashtable 하나더 , sorted set -> skiplist와 hashTable
        - Ziplist를 이용하자
        - In memory 특성 상 적은 개수라면 선형 탐색을 하더라도 빠르다.
        - ziplist로 대체해서 처리하는 설정이 존재한다
- o(N)은 조심하자
    - Redis는 Single Thread
    - Redis가 동시에 하나의 명령만 처리할 수 있다.
    - 단순 get / set 초당 10만 TPS 정도 가능
    - 긴 명령을 쓰면 안됨
        - keys
            - scan으로 처리
        - flushall, flushdb
        - delete collections -> 백만개 정도 되면 1~2초 걸림
        - get all collections -> 느려진당
    - Collection의 모든 item을 가져와야 할때
        - 큰 Collection을 작은 여러개의 Collection으로 나눠서 저장
        - 몇천개 안쪽으로 저장하자
- Redis Replication
    - A서버의 데이터를 B서버도 가지고 있다
    - Async Replication
        - Replication Lag이 발생한다 -> 데이터가 바뀔때 살짝의 타이밍이 차이가있음
    - 'Replicaof' or 'slaveof' 명령으로 설정
        - secondary에서 설정한다
        - Replicaof hostname port
    - dbms로 보면 statement replication가 유사
    - 주의할점
        - fork 사용이라 메모리 부족일 수 도 있음
        - Aws 는 좀 안정적

- redis.conf 권장 설정
    - Maxclient 설정 50000
    - RDB/AOF 설정 off
    - 특정 commands disable
        - keys -> elasticcache는 이미 막혀있음
    - 적절한 ziplist 설정

## Shading
- 데이터를 어떻게 나눌 것인가?
    - range
        - 그냥 특정 range를 정의하고 range에 속하면 거기에 저장
        - 서버의 사용량이 극심하게 나뉨
        - 그렇다고 키를 바꿀순 없음
- 데이터를 어떻게 찾을 것인가?

## Redis Cluster
    - Hash 알고리즘 CRC16을 사용 -> % 16384

## Monitoring
- Redis Info
    - RSS 피지컬 메모리
    - Used memory
    - Connection 수
    - 초당 처리 요청 수 tps
- System
    - cpu
    - disk
    - network rx/tx -> 네트워크가 너무많으면 문제
- CPU 100 %칠 경우
    - cpu 업그레이드
- O(N) 계열 
    - monitor 명령을 통해 특정 패턴을 파악하는 것이 필요
    - Monitor 잘못 쓰면 부하로 해당 서버에 더 큰 문제를 일으킬 수 있음
    - 짧게 잠깐 켜서 크래핑하자

## 결론
- Client-output-buffer-limit 설정이 필요
- 32기가 장비라면 24기가 이하로 쓰자
- 캐쉬일 경우는 문제가 적게 발생
    - Consistent Hashing 을 써도 부하는 각각 다름짐
- Persistent Store의 경우
    - primary / secondary 구조
    - 메모리 널널하게 사용하자
        - migration
        - 가능하면 자동화 툴을 만들어서 이용
    - 돈을 많이쓰장
