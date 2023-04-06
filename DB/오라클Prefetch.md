# Prefetch

- 디스크 블록을 읽을 때 곧이어 읽을 가능성이 높은 블록을 미리 읽어오는 기능

- 한번에 여러개 Single Block I/O를 병렬 방식으로 동시 수행

* Multi Block I/O가 한 익스텐트에 속한 인접한 블록들을 한꺼번에 읽는 방식이라면 Prefetch는 멀리 떨어져있는 블록들을 한꺼번에 읽는 방식 (서로 다른 익스텐트에 위치한 블록을 배치 방식으로 미리 적재)

* db file parallel read 대기 이벤트로 측정

- Index와 Table 간 Random Access 시 디스크에서 테이블의 다른 블록까지 미리 캐싱

## 장점
1. 한번 I/O Call이 발생 할때 서로 다른 익스텐트에 위치한 블록을 병렬 방식으로 동시에 여러 개 수행하는 것이므로 읽어야 할 블록들이 서로 다른 디스크 드라이브에 위치한다면 Prefetch에 의한 성능 향상은 더욱 좋음
2. 오라클은 미리 적재했을 때 효과를 얻을 수 있는 오퍼레이션에만 이 기능을 적용하고, 만약 Prefetch한 블록들이 실제 액세스로 연결되지 못한 채 캐시에서 밀려나는 비율이 높다면 더는 이 기능이 작동되지 못하도록 정지
3. 데이터 블록을 읽는 도중에 물리적인 디스크 I/O가 필요할 때면 서버 프로세스는 I/O 서브시스템에 I/O Call을 발생시키고 잠시 대기 상태에 빠진다.
4. 어차피 대기 상태에 잠시 쉬어야 하므로, 곧이어 읽을 가능성이 높은 블록들을 버퍼 캐시에 미리 적재해 놓는다면 대기 이벤트 발생횟수를 그만큼 줄일 수 있다.
5. Prefetch는 db file parallel read 대기 이벤트로 측정

Sequential 액세스 성능 향상 
- Multiblock I/O, 인덱스 Prefetch

Random 액세스 성능 향상 
- 버퍼 Pinning, 테이블 Prefetch

출처 : http://wiki.gurubee.net/display/STUDY/04.+Prefetch
